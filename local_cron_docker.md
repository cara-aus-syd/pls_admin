I found that adding a shell script that contains the command:

```bash
docker exec -d adminpls python3 -m flask scheduler
```
to a local cron job would result in the docker command not actually executing.

I fixed this by adding the local logged in user (${USER}) to the docker group using the comand:

```shell
sudo usermod -aG docker ${USER}
```
Then logging out and logging back in as ${USER}.

Once I did this, the cron job would run the script containing the docker command and actually execute the docker command instead of seemingly skipping over it.
