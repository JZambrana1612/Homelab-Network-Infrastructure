# 🛠️ Create & Mount LXC Storage on Proxmox (14GB Partition)

This section documents how I created a dedicated 14 GB logical volume for container storage in Proxmox, made it persistent, and added it to the Proxmox GUI.

---

## 📊 Step 0: Check Available Storage in Your LVM Volume Group

Before creating a new logical volume, check if you have free space available in your existing volume group (usually `pve`):

```bash
vgs
```

Example output:
```
VG   #PV #LV #SN Attr   VSize    VFree
pve    1   3   0 wz--n- <237.47g  <16.00g
```

You can also run:

```bash
lvs
```

This shows how the space is currently allocated across logical volumes.
Ex.
--
![Space Available](images/VFree_space.png)

> ✅ Look for the `VFree` column in `vgs` — if it shows at least 14G free, you're good to proceed with creating your storage volume.

---

## 🧱 Step 1: Create a New Logical Volume (LV)

Using 14 GB of free space in the existing `pve` Volume Group:

```bash
lvcreate -L 14G -n lxc-storage pve
```

---

## 🧼 Step 2: Format the Logical Volume

Format the new LV using the `ext4` filesystem:

```bash
mkfs.ext4 /dev/pve/lxc-storage
```

---

## 📂 Step 3: Create Mount Point & Mount It

Create a directory where the LV will be mounted:

```bash
mkdir /mnt/lxc-storage
```

Mount it:

```bash
mount /dev/pve/lxc-storage /mnt/lxc-storage
```

---

## 🔁 Step 4: Make the Mount Persistent

Open `/etc/fstab`:

```bash
nano /etc/fstab
```

Add the following line to the bottom of the file:

```
/dev/pve/lxc-storage /mnt/lxc-storage ext4 defaults 0 2
```

Then test the mount and confirm it works:

```bash
umount /mnt/lxc-storage
mount -a
df -h /mnt/lxc-storage
```

---

## 🖥️ Step 5: Add the New Storage to Proxmox GUI

Go to:
**Datacenter → Storage → Add → Directory**

Then fill out the following:

| Field         | Value                |
|---------------|----------------------|
| ID            | `lxc-storage`        |
| Directory     | `/mnt/lxc-storage`   |
| Content       | `Container` (check it) |
| Nodes         | `pve`                |
| Shared        | Leave unchecked      |

Click **Add**.

---

## ✅ Outcome

You now have:
- A dedicated **14 GB LXC storage volume**
- **Mounted persistently** at `/mnt/lxc-storage`
- **Available in the Proxmox GUI** for container creation
