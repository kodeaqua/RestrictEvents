---
name: Bug report
about: Something does not work as documented
labels: bug
---

**Hardware / macOS**
- Model identifier (real or spoofed):
- CPU:
- macOS version and build:
- RestrictEvents version:

**Boot arguments and NVRAM**
Include `revpatch`, `revblock`, `revcpu`, `revcpuname` if set.

**What happened vs. what you expected**

**Logs**
Use a DEBUG build with `-revdbg -revproc` and attach the output of:

    log show --last boot | grep -E "rev|supd"
