# Setting Up Account and Logging into the Server

1. To register with Compute Canada (CC), you need a valid **CCRI**.
2. Once the CCRI is received, register here: [https://ccdb.alliancecan.ca/](https://ccdb.alliancecan.ca/)
3. Create your **username and password**.
4. The system requires you to set up **multi-factor authentication** at this link:  
   [https://ccdb.alliancecan.ca/multi_factor_authentications](https://ccdb.alliancecan.ca/multi_factor_authentications)
5. Once you have your username and password, log into one of the CC servers (e.g., **Béluga**) using SSH:

   ```bash
   ssh <username>@beluga.alliancecan.ca
   ```

   The system will prompt you for a password and a login approval via **Duo Push** on your phone.

> ⚠️ **Note**: The **username is not your CCI**!  
> It is the name of the account, and you can find it on the CCDB **Home** page.

---

## Currently Available Compute Canada Servers

| Cluster | CPU Architecture          | Max RAM/node | GPUs Available | Best For                                                     |
|---------|---------------------------|--------------|----------------|--------------------------------------------------------------|
| Cedar   | Intel Broadwell/Skylake   | Up to 512 GB | V100, A100     | General-purpose bioinformatics, well-balanced system         |
| Béluga  | Intel Skylake             | Up to 768 GB | V100           | RAM-heavy tasks, newer hardware, faster interconnect         |
| Graham  | Skylake (some Broadwell)  | Up to 512 GB | P100, V100     | CPU/GPU hybrid workloads, lighter loads                      |
| Narval  | AMD EPYC (Rome/Milan)     | Up to 1 TB+  | A100           | Newest, fastest CPU nodes; good for memory-heavy analyses    |

---

## Storage Directories on Login

Once logged in, you will see three directories:

- `nearline/`
- `projects/`
- `scratch/`

### Purpose of Each Directory

| Feature   | `projects/`            | `scratch/`               | `nearline/`               |
|-----------|------------------------|---------------------------|----------------------------|
| Use Case  | Long-term, shared      | Temporary, fast I/O       | Cold archive               |
| Backup    | Sometimes              | ❌ No                     | ❌ No                      |
| Retention | Persistent             | Purged after 30–60 days   | Persistent                 |
| Speed     | Medium-Fast            | ⚡ Very fast               | 🐢 Slow                    |
| Quota     | PI-based               | Per-user, large           | Per-user, very large       |

---

## 🧬 Best Practice Example for RNA-seq

- Store **raw FASTQ files** in `nearline/`
- Copy FASTQs to `scratch/` for alignment
- Store final **BAMs, counts, and scripts** in `projects/`

    
