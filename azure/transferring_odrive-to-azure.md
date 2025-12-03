# How to Transfer Data from the **O Drive** to **Azure Storage**

This guide walks you through mounting the O drive, setting up an Azure
File Share, and transferring your data safely.

------------------------------------------------------------------------

## 🚀 1. Mount the O Drive

### **On DTU computers**

The O drive is usually available automatically.\
Just log in with your DTU username and password.

### **On macOS**

The O drive can be accessed at:

    /Volumes/nnfcb

------------------------------------------------------------------------

## ☁️ 2. Set Up Your Azure File Share

Go to your **Azure Storage Account**\
(You can also use a storage account provided via the Seqera group).

### **Create a new File Share**

Navigate in the Azure portal:

1.  **Data Storage** → **File Shares**
2.  Click **New File Share**
3.  Fill out **Basics**
4.  Select **No Backup**
5.  Click **Review + create**
6.  Deploy the resource

Once it's created (e.g., named **Data1**), you can proceed to connect
it.

------------------------------------------------------------------------

## 🔗 3. Connect the File Share to Your Machine

1.  In the File Share overview, click the **⋯ (three dots)** next to its
    name.
2.  Select **Connect**.
3.  Choose your **Operating System**.
4.  Azure will show you a script.
5.  **Copy the script** and run it on your computer or your Virtual
    Machine.

> 💡 *Tip:*\
> Use your local computer for smaller transfers.\
> For large datasets, a VM is faster and prevents local bandwidth
> issues.

------------------------------------------------------------------------

## 📁 4. Transfer Your Data

With both drives mounted, simply use the `cp` command (macOS/Linux):

``` bash
cp -r /Volumes/nnfcb/file1 /Volumes/Data1
```

Replace `file1` and `Data1` with your actual paths.

------------------------------------------------------------------------

## 🧹 5. Cleanup (Good Practice)

Once the transfer is complete and verified in Azure:

-   Move the files into their final location inside Azure Storage.
-   **Delete the files** from the File Share to avoid unnecessary
    storage costs.

------------------------------------------------------------------------
