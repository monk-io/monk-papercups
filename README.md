# Papercups & Monk

This repository contains Monk.io template to deploy Papercups system either locally or on cloud of your choice (AWS, GCP, Azure, Digital Ocean).

## Local Deployment

This template is available directly from Monkhub.io therefore if you want a quick deploy simply run below command after launching `monkd`:

```bash
➜  monk-papercups git:(main) ✗ monk login

➜  monk-papercups git:(main) ✗ monk run papercups/stack

✔ Started papercups/stack

✨ All done!

🔩 papercups/stack
 └─🧊 local
    ├─📦 templates-local-papercups-papercups-papercups
    │  ├─🧩 papercups/papercups:latest
    │  ├─🔌 open localhost:80 -> 80
    │  ├─🔌 open localhost:3000 -> 3000
    │  └─🔌 open localhost:4000 -> 4000
    └─📦 templates-local-papercups-postgres-postgres
       ├─🧩 postgres:12
       ├─💾 /Users/toymachine/.monk/volumes/db_data -> /var/lib/postgresql/data
       └─🔌 open localhost:5432 (0.0.0.0:5432) -> 5432
```

## Cloud Deployment

To deploy the above system to your cloud provider, create a new Monk cluster and provision your instances.

```bash
➜  monk-papercups git:(main) ✗ monk cluster new
? New cluster name papercups-deployment
✔ Cluster created
Your cluster has been created successfully.

➜  monk-papercups git:(main) ✗ monk cluster provider add
? Cloud provider gcp
? GOOGLE_APPLICATION_CREDENTIALS is set. Try load it? Yes
✔ Provider added successfully

➜  monk-papercups git:(main) ✗ monk cluster grow -p gcp
? Name for the new instance my-instance
? Tags (split by whitespace) papercups
? Instance region (gcp) europe-west2
? Instance zone (gcp) europe-west2-c
? Instance type (gcp) n2-standard-2
? Disk Size (GBs) 10
? Number of instances (or press ENTER to use default = 1) 2
✔ Creating a new instance(s) on gcp...
✔ Syncing nodes DONE
✔ Cluster grown successfully
```

Once cluster is ready execute the same command as for local and select your cluster (the option will appear automatically).

```bash
➜  monk-papercups git:(main) ✗ monk run papercups/stack
? Select tag to run on: papercups
```

### Logs & Shell

```bash
➜  monk logs -l 1000 -f papercups/papercups

➜  monk shell papercups/papercups
```
