
By running

```proverif ./sitp.pv```

you can switch between attack scenarios by enabling or removing the comments in sitp.pv:

```
    (* No Attack *)
    ( (processServer(victim_user)) | (processClient(victim_user)) )

    (* Client Impersonation Attack *)
    (* (processServer(victim_user)) | (processClient(attacker_user)) *)

    (* Server Impersonation Attack *)
    (* (processServer(attacker_user)) | (processClient(victim_user)) *)

```
