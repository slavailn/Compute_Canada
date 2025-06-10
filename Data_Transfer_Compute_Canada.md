# 🚀 Data Transfer to Compute Canada Clusters

## 1. Use Data Transfer Nodes (DTNs)
- Avoid login nodes for file transfers — use nodes like `beluga-dtn`, `cedar-dtn`, `narval-dtn`.
- Tools like **Globus**, **rsync**, **scp**, and **sftp** operate via DTNs for better speed and reliability.

---

## 2. Methods for Data Transfer

### 🛠️ 2.1 Globus
- Best for large or remote transfers.
- Uses DTNs automatically, with built-in data integrity and resume.
- Authenticate with your Compute Canada account and transfer via GUI.

### 🔄 2.2 rsync
- Best for syncing folders and resuming large transfers.

#### 🔁 Upload with compression and progress:
```bash
rsync -avzh --no-g --no-p --partial --progress <LOCAL> username@beluga.alliancecan.ca:/home/username/scratch/somedir/
```

#### 🔁 Download from cluster:
```bash
rsync -avzh --partial --progress username@beluga.alliancecan.ca:/home/username/scratch/somedir/ ./somedir/
```

- `-a`: archive mode  
- `-v`: verbose  
- `-z`: compress  
- `-h`: human-readable  
- `--partial`: keep partially transferred files  
- `--progress`: show progress  
- `--no-g`, `--no-p`: do not preserve group/permissions

### 🔐 2.3 SCP (Secure Copy)

#### 📥 Upload file:
```bash
scp myfile.fastq username@beluga-dtn.alliancecan.ca:/project/myproject/
```

#### 📂 Upload folder:
```bash
scp -r mydata/ username@cedar-dtn.alliancecan.ca:/project/myproject/data/
```

#### 📤 Download file:
```bash
scp username@graham-dtn.alliancecan.ca:/project/myproject/results/output.txt .
```

### 📁 2.4 SFTP (Secure FTP)

#### 🔗 Start SFTP session:
```bash
sftp username@narval-dtn.alliancecan.ca
```

#### 📂 Inside SFTP session:
```sftp
cd /project/myproject/
put myfile.txt
get output.txt
mkdir results
exit
```

---

## 3. Best Practices 🧠

- **Use DTNs** (not login nodes) for all data transfers.
- Use `/scratch` or `/project` as the destination path.
- Globus for big jobs, `rsync` for efficient syncs, `scp/sftp` for small tasks.
- Always verify file integrity (Globus does it automatically).

---

## 📂 Transfer Method Comparison

| Method   | Best For                            | Pros                        | Cons                             |
|----------|-------------------------------------|------------------------------|----------------------------------|
| Globus   | Large transfers, remote syncing     | Fast, reliable, resumable   | Requires setup/login             |
| rsync    | Folder syncs, resuming transfers    | Efficient, resumable        | Requires command-line            |
| scp      | Small file transfers                | Simple, fast for small jobs | No resume on failure             |
| sftp     | Interactive file browsing/upload    | GUI support, secure         | No resume, slower                |
