# Configure Kerberos Authentication

This section explains how to integrate insight.io with Kerberos authentication. You can skip this part if you are not using Kerberos authentication.

Log into the machine that host the KDC server and add a principle called `git`, if not existed already:

```bash
kadmin.local
```

```bash
addprinc git
```

```bash
ktadd -norandkey git
```

Log into the machine that you are planning to run insight.io with, change to user `root`, and generate a valid kerberos ticket.

```bash
sudo su root
```

```bash
kinit git
```

Then the Kerberos authentication part is all-set. insight.io will automatically use the newly generated ticket as authorization credentials. But please make sure the ticket is always valid by manually setting the ticket expiration time or periodically running `kinit`. 
