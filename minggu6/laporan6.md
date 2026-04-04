### Laporan Praktikum 6

<h4>Nama    : Reyhandhika Zikri Prijadi<h4>
<h4>Nim     : 254107020219<h4>
<h4>Kelas   : TI-1G<h4>

## Praktikum 6.1 - Melihat Proses dan Thread

1. Tampilkan semua proses yang berjalan:
```bash
ps aux
```
Output:
```bash
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.1  0.6  22080 13264 ?        Ss   10:23   0:05 /sbin/init
root           2  0.0  0.0      0     0 ?        S    10:23   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        S    10:23   0:00 [pool_workqueue_release]
root           4  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-rcu_g]
root           5  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-rcu_p]
root           6  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-slub_]
root           7  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-netns]
root          10  0.0  0.0      0     0 ?        I<   10:23   0:01 [kworker/0:0H-kblockd]
root          12  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-mm_pe]
root          13  0.0  0.0      0     0 ?        I    10:23   0:00 [rcu_tasks_kthread]
root          14  0.0  0.0      0     0 ?        I    10:23   0:00 [rcu_tasks_rude_kthread]
root          15  0.0  0.0      0     0 ?        I    10:23   0:00 [rcu_tasks_trace_kthread]
root          16  0.0  0.0      0     0 ?        S    10:23   0:00 [ksoftirqd/0]
root          17  0.0  0.0      0     0 ?        I    10:23   0:00 [rcu_preempt]
root          18  0.0  0.0      0     0 ?        S    10:23   0:00 [migration/0]
root          19  0.0  0.0      0     0 ?        S    10:23   0:00 [idle_inject/0]
root          20  0.0  0.0      0     0 ?        S    10:23   0:00 [cpuhp/0]
root          21  0.0  0.0      0     0 ?        S    10:23   0:00 [kdevtmpfs]
root          22  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-inet_]
root          23  0.0  0.0      0     0 ?        S    10:23   0:00 [kauditd]
root          24  0.0  0.0      0     0 ?        S    10:23   0:00 [khungtaskd]
root          26  0.0  0.0      0     0 ?        S    10:23   0:00 [oom_reaper]
root          27  0.0  0.0      0     0 ?        I    10:23   0:00 [kworker/u2:2-events_power_efficient]
root          28  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-write]
root          29  0.0  0.0      0     0 ?        S    10:23   0:00 [kcompactd0]
root          30  0.0  0.0      0     0 ?        SN   10:23   0:00 [ksmd]
root          31  0.0  0.0      0     0 ?        SN   10:23   0:00 [khugepaged]
root          32  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-kinte]
root          33  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-kbloc]
root          34  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-blkcg]
root          35  0.0  0.0      0     0 ?        S    10:23   0:00 [irq/9-acpi]
root          36  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-tpm_d]
root          37  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-ata_s]
root          38  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-md]
root          39  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-md_bi]
root          40  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-edac-]
root          41  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-devfr]
root          42  0.0  0.0      0     0 ?        S    10:23   0:00 [watchdogd]
root          45  0.0  0.0      0     0 ?        S    10:23   0:00 [kswapd0]
root          46  0.0  0.0      0     0 ?        S    10:23   0:00 [ecryptfs-kthread]
root          47  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-kthro]
root          48  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-acpi_]
root          49  0.0  0.0      0     0 ?        S    10:23   0:00 [scsi_eh_0]
root          50  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-scsi_]
root          51  0.0  0.0      0     0 ?        S    10:23   0:00 [scsi_eh_1]
root          52  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-scsi_]
root          53  0.0  0.0      0     0 ?        I    10:23   0:00 [kworker/u2:3-events_power_efficient]
root          56  0.2  0.0      0     0 ?        I    10:23   0:10 [kworker/0:3-events]
root          57  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-mld]
root          58  0.0  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-ipv6_]
root          65  0.0  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-kstrp]
root          67  0.0  0.0      0     0 ?        I<   10:24   0:00 [kworker/u3:0]
root          72  0.0  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-crypt]
root          81  0.0  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-charg]
root         145  0.0  0.0      0     0 ?        S    10:24   0:00 [scsi_eh_2]
root         146  0.0  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-scsi_]
root         159  0.0  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-kdmfl]
root         188  0.0  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-raid5]
root         228  0.0  0.0      0     0 ?        S    10:24   0:00 [jbd2/dm-0-8]
root         229  0.0  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-ext4-]
root         317  0.0  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-kmpat]
root         318  0.0  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-kmpat]
root         349  0.0  1.3 289116 27452 ?        SLsl 10:24   0:00 /sbin/multipathd -d -s
root         370  0.0  0.3  29052  7888 ?        Ss   10:24   0:00 /usr/lib/systemd/systemd-udevd
root         371  0.0  0.0      0     0 ?        S    10:24   0:00 [psimon]
root         433  0.0  0.0      0     0 ?        S    10:24   0:00 [irq/18-vmwgfx]
root         434  0.0  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-ttm]
root         475  0.0  0.0      0     0 ?        S    10:24   0:00 [jbd2/sda2-8]
root         476  0.0  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-ext4-]
systemd+     519  0.0  0.4  19012  9484 ?        Ss   10:24   0:00 /usr/lib/systemd/systemd-networkd
systemd+     529  0.0  0.6  21592 13136 ?        Ss   10:24   0:00 /usr/lib/systemd/systemd-resolved
systemd+     531  0.0  0.3  91028  7960 ?        Ssl  10:24   0:00 /usr/lib/systemd/systemd-timesyncd
root         570  0.0  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-cfg80]
message+     648  0.0  0.2   9816  5656 ?        Ss   10:24   0:00 @dbus-daemon --system --address=systemd: --nofork --nopidfile
polkitd      652  0.0  0.4 383704  9920 ?        Ssl  10:24   0:00 /usr/lib/polkit-1/polkitd --no-debug
root         659  0.0  0.4  18200  8960 ?        Ss   10:24   0:00 /usr/lib/systemd/systemd-logind
root         661  0.0  0.6 468980 13732 ?        Ssl  10:24   0:00 /usr/libexec/udisks2/udisksd
syslog       682  0.0  0.3 222508  6208 ?        Ssl  10:24   0:00 /usr/sbin/rsyslogd -n -iNONE
root         701  0.0  0.6 392100 12952 ?        Ssl  10:24   0:00 /usr/sbin/ModemManager
root         706  0.0  0.1   6824  2908 ?        Ss   10:24   0:00 /usr/sbin/cron -f -P
root         709  0.0  1.1 109684 23140 ?        Ssl  10:24   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-up
root         742  0.0  0.2   6976  4876 tty1     Ss   10:24   0:00 /bin/login -p --
root         913  0.0  0.0      0     0 ?        S    10:24   0:00 [psimon]
reyhand+     915  0.0  0.5  20180 11320 ?        Ss   10:24   0:00 /usr/lib/systemd/systemd --user
reyhand+     916  0.0  0.1  21156  3588 ?        S    10:24   0:00 (sd-pam)
reyhand+     927  0.0  0.2   8656  5636 tty1     S+   10:24   0:00 -bash
root         950  0.0  0.4  12024  8252 ?        Ss   10:25   0:00 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
root        1024  0.0  0.0      0     0 ?        I    10:33   0:00 [kworker/u2:5-events_power_efficient]
root        1025  0.0  0.0      0     0 ?        I    10:33   0:00 [kworker/u2:6-events_unbound]
root        1029  0.0  0.8  66728 17624 ?        S<s  10:33   0:01 /usr/lib/systemd/systemd-journald
root        1036  0.2  0.0      0     0 ?        I<   11:23   0:01 [kworker/0:1H-kblockd]
root        1065  0.4  2.0 478096 41936 ?        Ssl  11:23   0:03 /usr/libexec/fwupd/fwupd
root        1072  0.2  0.4 314204  9364 ?        Ssl  11:23   0:01 /usr/libexec/upowerd
root        1086  0.0  0.5  14968 10572 ?        Ss   11:24   0:00 sshd: reyhandhika [priv]
reyhand+    1146  0.1  0.3  14968  7096 ?        S    11:24   0:00 sshd: reyhandhika@pts/0
reyhand+    1147  0.0  0.2   8648  5652 pts/0    Ss   11:24   0:00 -bash
root        1167  0.0  0.0      0     0 ?        I    11:28   0:00 [kworker/0:1-events]
reyhand+    1175  314  0.2  10884  4588 pts/0    R+   11:35   0:00 ps aux
```
2. Tampilkan proses beserta thread-nya, dapat dilihat pada kolom LWP (LightWeight Process ID):
```bash
ps aux -L
```

Output:
```bash
USER         PID     LWP %CPU NLWP %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1       1  0.1    1  0.6  22080 13264 ?        Ss   10:23   0:05 /sbin/init
root           2       2  0.0    1  0.0      0     0 ?        S    10:23   0:00 [kthreadd]
root           3       3  0.0    1  0.0      0     0 ?        S    10:23   0:00 [pool_workqueue_release]
root           4       4  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-rcu_g]
root           5       5  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-rcu_p]
root           6       6  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-slub_]
root           7       7  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-netns]
root          10      10  0.0    1  0.0      0     0 ?        I<   10:23   0:01 [kworker/0:0H-kblockd]
root          12      12  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-mm_pe]
root          13      13  0.0    1  0.0      0     0 ?        I    10:23   0:00 [rcu_tasks_kthread]
root          14      14  0.0    1  0.0      0     0 ?        I    10:23   0:00 [rcu_tasks_rude_kthread]
root          15      15  0.0    1  0.0      0     0 ?        I    10:23   0:00 [rcu_tasks_trace_kthread]
root          16      16  0.0    1  0.0      0     0 ?        S    10:23   0:01 [ksoftirqd/0]
root          17      17  0.0    1  0.0      0     0 ?        I    10:23   0:00 [rcu_preempt]
root          18      18  0.0    1  0.0      0     0 ?        S    10:23   0:00 [migration/0]
root          19      19  0.0    1  0.0      0     0 ?        S    10:23   0:00 [idle_inject/0]
root          20      20  0.0    1  0.0      0     0 ?        S    10:23   0:00 [cpuhp/0]
root          21      21  0.0    1  0.0      0     0 ?        S    10:23   0:00 [kdevtmpfs]
root          22      22  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-inet_]
root          23      23  0.0    1  0.0      0     0 ?        S    10:23   0:00 [kauditd]
root          24      24  0.0    1  0.0      0     0 ?        S    10:23   0:00 [khungtaskd]
root          26      26  0.0    1  0.0      0     0 ?        S    10:23   0:00 [oom_reaper]
root          27      27  0.0    1  0.0      0     0 ?        I    10:23   0:00 [kworker/u2:2-events_power_efficient]
root          28      28  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-write]
root          29      29  0.0    1  0.0      0     0 ?        S    10:23   0:00 [kcompactd0]
root          30      30  0.0    1  0.0      0     0 ?        SN   10:23   0:00 [ksmd]
root          31      31  0.0    1  0.0      0     0 ?        SN   10:23   0:00 [khugepaged]
root          32      32  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-kinte]
root          33      33  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-kbloc]
root          34      34  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-blkcg]
root          35      35  0.0    1  0.0      0     0 ?        S    10:23   0:00 [irq/9-acpi]
root          36      36  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-tpm_d]
root          37      37  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-ata_s]
root          38      38  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-md]
root          39      39  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-md_bi]
root          40      40  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-edac-]
root          41      41  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-devfr]
root          42      42  0.0    1  0.0      0     0 ?        S    10:23   0:00 [watchdogd]
root          45      45  0.0    1  0.0      0     0 ?        S    10:23   0:00 [kswapd0]
root          46      46  0.0    1  0.0      0     0 ?        S    10:23   0:00 [ecryptfs-kthread]
root          47      47  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-kthro]
root          48      48  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-acpi_]
root          49      49  0.0    1  0.0      0     0 ?        S    10:23   0:00 [scsi_eh_0]
root          50      50  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-scsi_]
root          51      51  0.0    1  0.0      0     0 ?        S    10:23   0:00 [scsi_eh_1]
root          52      52  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-scsi_]
root          53      53  0.0    1  0.0      0     0 ?        I    10:23   0:01 [kworker/u2:3-events_unbound]
root          56      56  0.2    1  0.0      0     0 ?        I    10:23   0:12 [kworker/0:3-events]
root          57      57  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-mld]
root          58      58  0.0    1  0.0      0     0 ?        I<   10:23   0:00 [kworker/R-ipv6_]
root          65      65  0.0    1  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-kstrp]
root          67      67  0.0    1  0.0      0     0 ?        I<   10:24   0:00 [kworker/u3:0]
root          72      72  0.0    1  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-crypt]
root          81      81  0.0    1  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-charg]
root         145     145  0.0    1  0.0      0     0 ?        S    10:24   0:00 [scsi_eh_2]
root         146     146  0.0    1  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-scsi_]
root         159     159  0.0    1  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-kdmfl]
root         188     188  0.0    1  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-raid5]
root         228     228  0.0    1  0.0      0     0 ?        S    10:24   0:00 [jbd2/dm-0-8]
root         229     229  0.0    1  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-ext4-]
root         317     317  0.0    1  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-kmpat]
root         318     318  0.0    1  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-kmpat]
root         349     349  0.0    7  1.3 289116 27452 ?        SLsl 10:24   0:00 /sbin/multipathd -d -s
root         349     357  0.0    7  1.3 289116 27452 ?        SLsl 10:24   0:00 /sbin/multipathd -d -s
root         349     358  0.0    7  1.3 289116 27452 ?        SLsl 10:24   0:00 /sbin/multipathd -d -s
root         349     359  0.0    7  1.3 289116 27452 ?        SLsl 10:24   0:00 /sbin/multipathd -d -s
root         349     360  0.0    7  1.3 289116 27452 ?        SLsl 10:24   0:00 /sbin/multipathd -d -s
root         349     361  0.0    7  1.3 289116 27452 ?        SLsl 10:24   0:00 /sbin/multipathd -d -s
root         349     362  0.0    7  1.3 289116 27452 ?        SLsl 10:24   0:00 /sbin/multipathd -d -s
root         370     370  0.0    1  0.3  29052  7888 ?        Ss   10:24   0:00 /usr/lib/systemd/systemd-udevd
root         371     371  0.0    1  0.0      0     0 ?        S    10:24   0:00 [psimon]
root         433     433  0.0    1  0.0      0     0 ?        S    10:24   0:00 [irq/18-vmwgfx]
root         434     434  0.0    1  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-ttm]
root         475     475  0.0    1  0.0      0     0 ?        S    10:24   0:00 [jbd2/sda2-8]
root         476     476  0.0    1  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-ext4-]
systemd+     519     519  0.0    1  0.4  19012  9484 ?        Ss   10:24   0:00 /usr/lib/systemd/systemd-networkd
systemd+     529     529  0.0    1  0.6  21592 13136 ?        Ss   10:24   0:00 /usr/lib/systemd/systemd-resolved
systemd+     531     531  0.0    2  0.3  91028  7960 ?        Ssl  10:24   0:00 /usr/lib/systemd/systemd-timesyncd
systemd+     531     563  0.0    2  0.3  91028  7960 ?        Ssl  10:24   0:00 /usr/lib/systemd/systemd-timesyncd
root         570     570  0.0    1  0.0      0     0 ?        I<   10:24   0:00 [kworker/R-cfg80]
message+     648     648  0.0    1  0.2   9816  5656 ?        Ss   10:24   0:00 @dbus-daemon --system --address=systemd: --nofor
polkitd      652     652  0.0    4  0.4 383704  9920 ?        Ssl  10:24   0:00 /usr/lib/polkit-1/polkitd --no-debug
polkitd      652     688  0.0    4  0.4 383704  9920 ?        Ssl  10:24   0:00 /usr/lib/polkit-1/polkitd --no-debug
polkitd      652     689  0.0    4  0.4 383704  9920 ?        Ssl  10:24   0:00 /usr/lib/polkit-1/polkitd --no-debug
polkitd      652     690  0.0    4  0.4 383704  9920 ?        Ssl  10:24   0:00 /usr/lib/polkit-1/polkitd --no-debug
root         659     659  0.0    1  0.4  18200  8960 ?        Ss   10:24   0:00 /usr/lib/systemd/systemd-logind
root         661     661  0.0    6  0.6 468980 13732 ?        Ssl  10:24   0:00 /usr/libexec/udisks2/udisksd
root         661     676  0.0    6  0.6 468980 13732 ?        Ssl  10:24   0:00 /usr/libexec/udisks2/udisksd
root         661     679  0.0    6  0.6 468980 13732 ?        Ssl  10:24   0:00 /usr/libexec/udisks2/udisksd
root         661     681  0.0    6  0.6 468980 13732 ?        Ssl  10:24   0:00 /usr/libexec/udisks2/udisksd
root         661     702  0.0    6  0.6 468980 13732 ?        Ssl  10:24   0:00 /usr/libexec/udisks2/udisksd
root         661     707  0.0    6  0.6 468980 13732 ?        Ssl  10:24   0:00 /usr/libexec/udisks2/udisksd
syslog       682     682  0.0    4  0.3 222508  6208 ?        Ssl  10:24   0:00 /usr/sbin/rsyslogd -n -iNONE
syslog       682     712  0.0    4  0.3 222508  6208 ?        Ssl  10:24   0:00 /usr/sbin/rsyslogd -n -iNONE
syslog       682     713  0.0    4  0.3 222508  6208 ?        Ssl  10:24   0:00 /usr/sbin/rsyslogd -n -iNONE
syslog       682     714  0.0    4  0.3 222508  6208 ?        Ssl  10:24   0:00 /usr/sbin/rsyslogd -n -iNONE
root         701     701  0.0    4  0.6 392100 12952 ?        Ssl  10:24   0:00 /usr/sbin/ModemManager
root         701     716  0.0    4  0.6 392100 12952 ?        Ssl  10:24   0:00 /usr/sbin/ModemManager
root         701     717  0.0    4  0.6 392100 12952 ?        Ssl  10:24   0:00 /usr/sbin/ModemManager
root         701     720  0.0    4  0.6 392100 12952 ?        Ssl  10:24   0:00 /usr/sbin/ModemManager
root         706     706  0.0    1  0.1   6824  2908 ?        Ss   10:24   0:00 /usr/sbin/cron -f -P
root         709     709  0.0    2  1.1 109684 23140 ?        Ssl  10:24   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/
root         709     787  0.0    2  1.1 109684 23140 ?        Ssl  10:24   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/
root         742     742  0.0    1  0.2   6976  4876 tty1     Ss   10:24   0:00 /bin/login -p --
root         913     913  0.0    1  0.0      0     0 ?        S    10:24   0:00 [psimon]
reyhand+     915     915  0.0    1  0.5  20180 11320 ?        Ss   10:24   0:00 /usr/lib/systemd/systemd --user
reyhand+     916     916  0.0    1  0.1  21156  3588 ?        S    10:24   0:00 (sd-pam)
reyhand+     927     927  0.0    1  0.2   8656  5636 tty1     S+   10:24   0:00 -bash
root         950     950  0.0    1  0.4  12024  8252 ?        Ss   10:25   0:00 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 s
root        1024    1024  0.0    1  0.0      0     0 ?        I    10:33   0:00 [kworker/u2:5-events_unbound]
root        1025    1025  0.0    1  0.0      0     0 ?        I    10:33   0:00 [kworker/u2:6-events_power_efficient]
root        1029    1029  0.0    1  0.8  66728 17624 ?        S<s  10:33   0:00 /usr/lib/systemd/systemd-journald
root        1036    1036  0.1    1  0.0      0     0 ?        I<   11:23   0:01 [kworker/0:1H-kblockd]
root        1065    1065  0.3    6  2.0 478096 41936 ?        Ssl  11:23   0:02 /usr/libexec/fwupd/fwupd
root        1065    1066  0.0    6  2.0 478096 41936 ?        Ssl  11:23   0:00 /usr/libexec/fwupd/fwupd
root        1065    1067  0.0    6  2.0 478096 41936 ?        Ssl  11:23   0:00 /usr/libexec/fwupd/fwupd
root        1065    1068  0.0    6  2.0 478096 41936 ?        Ssl  11:23   0:00 /usr/libexec/fwupd/fwupd
root        1065    1069  0.0    6  2.0 478096 41936 ?        Ssl  11:23   0:00 /usr/libexec/fwupd/fwupd
root        1065    1071  0.0    6  2.0 478096 41936 ?        Ssl  11:23   0:00 /usr/libexec/fwupd/fwupd
root        1072    1072  0.1    4  0.4 314204  9376 ?        Ssl  11:23   0:01 /usr/libexec/upowerd
root        1072    1074  0.0    4  0.4 314204  9376 ?        Ssl  11:23   0:00 /usr/libexec/upowerd
root        1072    1075  0.0    4  0.4 314204  9376 ?        Ssl  11:23   0:00 /usr/libexec/upowerd
root        1072    1076  0.0    4  0.4 314204  9376 ?        Ssl  11:23   0:00 /usr/libexec/upowerd
root        1086    1086  0.0    1  0.5  14968 10572 ?        Ss   11:24   0:00 sshd: reyhandhika [priv]
reyhand+    1146    1146  0.1    1  0.3  14968  7096 ?        S    11:24   0:01 sshd: reyhandhika@pts/0
reyhand+    1147    1147  0.0    1  0.2   8648  5656 pts/0    Ss   11:24   0:00 -bash
root        1167    1167  0.0    1  0.0      0     0 ?        I    11:28   0:00 [kworker/0:1-events]
root        1177    1177  0.0    1  0.0      0     0 ?        I    11:38   0:00 [kworker/0:0]
reyhand+    1178    1178  400    1  0.2  11016  4600 pts/0    R+   11:38   0:00 ps aux -L
```
3. Lihat PID shell aktif dan detail prosesnya:
```bash
echo $$
ps -p $$ -f
```

Output:
```bash
reyhandhika@reyhandhika:~$ echo $$
1147
reyhandhika@reyhandhika:~$ ps -p $$ -f
UID          PID    PPID  C STIME TTY          TIME CMD
reyhand+    1147    1146  0 11:24 pts/0    00:00:00 -bash
```
4. Lihat hierarki proses secara visual
```bash
pstree -p
```
Output:
```bash
systemd(1)─┬─ModemManager(701)─┬─{ModemManager}(716)
           │                   ├─{ModemManager}(717)
           │                   └─{ModemManager}(720)
           ├─cron(706)
           ├─dbus-daemon(648)
           ├─fwupd(1065)─┬─{fwupd}(1066)
           │             ├─{fwupd}(1067)
           │             ├─{fwupd}(1068)
           │             ├─{fwupd}(1069)
           │             └─{fwupd}(1071)
           ├─login(742)───bash(927)
           ├─multipathd(349)─┬─{multipathd}(357)
           │                 ├─{multipathd}(358)
           │                 ├─{multipathd}(359)
           │                 ├─{multipathd}(360)
           │                 ├─{multipathd}(361)
           │                 └─{multipathd}(362)
           ├─polkitd(652)─┬─{polkitd}(688)
           │              ├─{polkitd}(689)
           │              └─{polkitd}(690)
           ├─rsyslogd(682)─┬─{rsyslogd}(712)
           │               ├─{rsyslogd}(713)
           │               └─{rsyslogd}(714)
           ├─sshd(950)───sshd(1086)───sshd(1146)───bash(114+
           ├─systemd(915)───(sd-pam)(916)
           ├─systemd-journal(1029)
           ├─systemd-logind(659)
           ├─systemd-network(519)
           ├─systemd-resolve(529)
           ├─systemd-timesyn(531)───{systemd-timesyn}(563)
           ├─systemd-udevd(370)
           ├─udisksd(661)─┬─{udisksd}(676)
           │              ├─{udisksd}(679)
           │              ├─{udisksd}(681)
           │              ├─{udisksd}(702)
           │              └─{udisksd}(707)
           ├─unattended-upgr(709)───{unattended-upgr}(787)
           └─upowerd(1072)─┬─{upowerd}(1074)
                           ├─{upowerd}(1075)
                           └─{upowerd}(1076)
```
### Latihan 6.1
Jalankan ps aux dan amati outputnya
1. Berapa total proses yang berjalan? Proses apa yang memiliki PID
terkecil?
2. Jalankan pstree-p dan temukan proses bash Anda. Proses apa yang
menjadi induk (PPID) dari bash tersebut?
3. Bandingkan output ps aux dan ps aux-L. Apa perbedaan yang Anda
lihat

Jawaban:

1. Berdasarkan output yang saya peroleh:
Total proses yang berjalan adalah sekitar ±120 proses (berdasarkan jumlah baris pada output).
Proses dengan PID terkecil adalah /sbin/init dengan PID 1, yang merupakan proses awal saat sistem dijalankan dan menjadi induk bagi proses lainnya.

2. Perintah pstree -p digunakan untuk melihat hubungan antar proses dalam bentuk struktur pohon Berdasarkan hasil yang diperoleh:
Terdapat dua proses bash, yaitu:
bash(927) yang berasal dari login(742)
bash(1147) yang berasal dari koneksi SSH
Untuk bash yang digunakan pada terminal (pts/0), terlihat urutannya:
systemd → sshd → sshd → sshd → bash(1147)
Dengan demikian, proses induk (PPID) dari bash tersebut adalah sshd, karena bash dijalankan melalui koneksi SSH.

3. Perintah ps aux menampilkan daftar proses yang sedang berjalan, sedangkan ps aux -L menampilkan proses beserta thread yang dimiliki oleh masing-masing proses.
Perbedaan yang terlihat:

Output ps aux -L lebih banyak dibandingkan ps aux.
Pada ps aux -L, satu proses dapat muncul beberapa kali karena memiliki beberapa thread.
ps aux hanya menampilkan proses utama, sedangkan ps aux -L menampilkan detail hingga tingkat thread (lightweight process).


## Praktikum 6.2 — Mengamati Siklus Hidup Proses

1. Buat proses di background dan amati kondisinya:
```bash
sleep 60 &
ps aux | grep sleep
```
Output:
```bash
reyhandhika@reyhandhika:~$ sleep 60 &
[1] 1213

reyhandhika@reyhandhika:~$ ps aux | grep sleep
reyhand+    1213  0.0  0.1   5684  2108 pts/0    S    11:59   0:00 sleep 60
reyhand+    1218 33.3  0.1   6544  2332 pts/0    S+   12:00   0:00 grep --color=auto sleep
```
2. Amati perubahan exit code dari perintah yang berhasil dan gagal:
```bash
ls / tmp
echo " Sukses : $?"
ls / direktori - tidak - ada
echo " Gagal : $?"
```
Output:
```bash
reyhandhika@reyhandhika:~$ ls /tmp
echo "Sukses: $?"
snap-private-tmp
systemd-private-5e3f22ea6fa640e58880ff828a179cfa-fwupd.service-hSPjtb
systemd-private-5e3f22ea6fa640e58880ff828a179cfa-ModemManager.service-Rn4NM7
systemd-private-5e3f22ea6fa640e58880ff828a179cfa-polkit.service-9BWhGn
systemd-private-5e3f22ea6fa640e58880ff828a179cfa-systemd-logind.service-rHxUjV
systemd-private-5e3f22ea6fa640e58880ff828a179cfa-systemd-resolved.service-FiHe1O
systemd-private-5e3f22ea6fa640e58880ff828a179cfa-systemd-timesyncd.service-kfhDxU
systemd-private-5e3f22ea6fa640e58880ff828a179cfa-upower.service-xKBY3R
Sukses: 0
reyhandhika@reyhandhika:~$ ls /direktori-tidak-ada
echo "Gagal: $?"
ls: cannot access '/direktori-tidak-ada': No such file or directory
Gagal: 2
```
### Latihan 6.2
1. Jalankan sleep 120 & dan amati kolom STAT pada ps aux. Kondisi
apa yang ditampilkan? Mengapa proses sleep berada di kondisi tersebut?
2. Jalankan beberapa perintah yang berhasil dan yang gagal, lalu catat exit
code masing-masing. Pola apa yang Anda temukan?

Jawaban:
1. Proses sleep akan memiliki status S (sleeping) pada kolom STAT.
Hal ini terjadi karena perintah sleep membuat proses menunggu (idle) selama waktu tertentu (120 detik) tanpa melakukan aktivitas CPU. Karena proses hanya menunggu waktu habis, maka sistem menempatkannya dalam kondisi sleeping (interruptible sleep).
2. Dari percobaan tersebut dapat disimpulkan bahwa:
Exit code 0 menunjukkan bahwa perintah berhasil dijalankan.
Exit code selain 0 menunjukkan bahwa terjadi kesalahan (error).
Pola yang ditemukan:
Semua perintah yang berhasil selalu menghasilkan exit code 0, sedangkan perintah yang gagal menghasilkan exit code non-zero (misalnya 1, 2, dan lainnya tergantung jenis error).

## Praktikum 6.3 - Mengatur Prioritas Proses 

1. Jalankan proses dengan prioritas rendah:
```bash
nice-n 10 sleep 300 &
```
Output:
```bash
reyhandhika@reyhandhika:~$ nice-n 10 sleep 300 &
[1] 1259
```

2. Verifikasi nilai nice pada kolom NI:
```bash
ps aux | grep sleep
```
Output : reyhandhika@reyhandhika:~$ ps aux | grep sleep
reyhand+    1267  0.0  0.1   6544  2332 pts/0    S+   12:24   0:00 grep --color=auto sleep

3. Ubah nilai nice proses yang sudah berjalan:
```bash
renice -n 15 -p <PID >
ps -p <PID > -o pid , ni , cmd
```
Output :
```bash
reyhandhika@reyhandhika:~$ sleep 120 &
[1] 1287
reyhandhika@reyhandhika:~$ ps aux | grep sleep
reyhand+    1287  0.0  0.1   5684  2108 pts/0    S    12:29   0:00 sleep 120
reyhand+    1289  0.0  0.1   6544  2332 pts/0    S+   12:30   0:00 grep --color=auto sleep
reyhandhika@reyhandhika:~$ renice -n 15 -p 1287
1287 (process ID) old priority 0, new priority 15
reyhandhika@reyhandhika:~$ ps -p 1287 -o pid,ni,cmd
    PID  NI CMD
   1287  15 sleep 120
```
4. Bersihkan proses percobaan:
```bash
kill %1
```
Output:
```bash
reyhandhika@reyhandhika:~$ kill %1
-bash: kill: (1287) - No such process
[1]+  Done                    sleep 120
```

### Latihan 6.3
1. Jalankan nice-n 5 sleep 200 & dan verifikasi nilai NI-nya dengan
ps.
2. Ubah nilai nice menjadi 10 menggunakan renice, lalu verifikasi kembali.
3. Coba ubah nilai nice menjadi-5 tanpa sudo. Apa yang terjadi? Mengapa
Linux membatasi hal ini untuk user biasa

Jawaban:
1. Proses sleep 200 berhasil dijalankan dengan nilai nice 5.
Pada output ps, kolom NI menunjukkan nilai 5, yang berarti prioritas proses lebih rendah dibandingkan default (0).
2. Setelah dijalankan, nilai nice berubah menjadi 10.
Hal ini menunjukkan bahwa prioritas proses semakin rendah karena nilai nice semakin besar.
3. Perintah gagal dijalankan karena user biasa tidak memiliki izin untuk memberikan prioritas tinggi (nilai nice negatif). Linux membatasi hal ini untuk mencegah pengguna biasa menjalankan proses dengan prioritas tinggi yang dapat mengganggu kinerja sistem secara keseluruhan.

Output :
```bash
1. reyhandhika@reyhandhika:~$ nice -n 5 sleep 200 &
[1] 1302
reyhandhika@reyhandhika:~$ ps -o pid,ni,cmd
    PID  NI CMD
   1147   0 -bash
   1302   5 sleep 200
   1303   0 ps -o pid,ni,cmd
reyhandhika@reyhandhika:~$ renice
2. reyhandhika@reyhandhika:~$ renice -n 10 -p 1309
1309 (process ID) old priority 0, new priority 10
reyhandhika@reyhandhika:~$ ps -o pid,ni,cmd
    PID  NI CMD
   1147   0 -bash
   1309  10 sleep 120
   1311   0 ps -o pid,ni,cmd

```
## Praktikum 6.4 - Mengirim Sinyal Ke Proses
1. Buat Proses Percobaan:
```bash

sleep 500 &
sleep 600 &
sleep 700 &
ps aux | grep -v grep | grep sleep
```
Output: 
```bash
reyhandhika@reyhandhika:~$ sleep 500 &
[1] 1439
reyhandhika@reyhandhika:~$ sleep 600 &
[2] 1444
reyhandhika@reyhandhika:~$ sleep 700 &
[3] 1457
reyhandhika@reyhandhika:~$ ps aux | grep -v grep | grep sleep
reyhand+    1439  0.0  0.1   5684  2104 pts/0    S    12:48   0:00 sleep 500
reyhand+    1444  0.0  0.1   5684  2104 pts/0    S    12:49   0:00 sleep 600
reyhand+    1457  0.0  0.1   5684  2104 pts/0    S    12:49   0:00 sleep 700
```

2. Hentikan satu proses dengan SIGTERM dan verifikasi:
```bash
kill <PID - sleep -500 >
ps aux | grep -v grep | grep sleep
```
Output:
```bash
reyhandhika@reyhandhika:~$ kill 1439
reyhandhika@reyhandhika:~$ ps aux | grep -v grep | grep sleep
reyhand+    1429  0.0  0.1   5684  2104 pts/0    S    12:48   0:00 sleep 500
reyhand+    1430  0.0  0.1   5684  2104 pts/0    S    12:49   0:00 sleep 600
reyhand+    1431  0.0  0.1   5684  2104 pts/0    S    12:49   0:00 sleep 700
[4]+  Terminated              sleep 120
```
3. Jeda dan lanjutkan proses dengan SIGSTOP/SIGCONT:
```bash
kill - SIGSTOP <PID - sleep -600 >
ps aux | grep sleep # amati kolom STAT : berubah
menjadi T
kill - SIGCONT <PID - sleep -600 >
ps aux | grep sleep # STAT kembali ke S
```
Output :
```bash
reyhandhika@reyhandhika:~$ ps aux | grep -v grep | grep sleep
reyhand+    1429  0.0  0.1   5684  2104 pts/0    S    12:48   0:00 sleep 500
reyhand+    1430  0.0  0.1   5684  2104 pts/0    S    12:49   0:00 sleep 600
reyhand+    1431  0.0  0.1   5684  2104 pts/0    S    12:49   0:00 sleep 700
reyhand+    1444  0.0  0.1   5684  2108 pts/0    T    12:53   0:00 sleep 600

[4]+  Stopped                 sleep 600

reyhandhika@reyhandhika:~$ kill -SIGCONT 1444
reyhandhika@reyhandhika:~$ ps aux | grep -v grep | grep sleep
reyhand+    1429  0.0  0.1   5684  2104 pts/0    S    12:48   0:00 sleep 500
reyhand+    1430  0.0  0.1   5684  2104 pts/0    S    12:49   0:00 sleep 600
reyhand+    1431  0.0  0.1   5684  2104 pts/0    S    12:49   0:00 sleep 700
reyhand+    1444  0.0  0.1   5684  2108 pts/0    S    12:53   0:00 sleep 600
```

4. Hentikan semua proses sleep sekaligus:
```bash
pkill sleep
```
Output:
```bash
reyhandhika@reyhandhika:~$ pkill sleep
[2]   Terminated              sleep 600
[3]   Terminated              sleep 700
[4]-  Terminated              sleep 600
[5]+  Terminated              sleep 700
```

### Latihan 6.4
1. Jalankan sleep 400 &, kirim SIGSTOP, dan amati perubahan kolom STAT. Kondisi apa yang muncul?
2. Kirim SIGCONT dan verifikasi proses kembali berjalan.
3. Hentikan proses dengan SIGTERM lalu verifikasi sudah tidak ada. Kapan Anda memilih SIGKILL daripada SIGTERM?

Jawaban:
1. Pada kolom STAT muncul huruf T.
Kondisi T (stopped) menunjukkan bahwa proses sedang dihentikan sementara (paused) dan tidak berjalan, karena menerima sinyal SIGSTOP.
```bash
reyhandhika@reyhandhika:~$ sleep 400 &
[1] 1463
reyhandhika@reyhandhika:~$ kill -SIGSTOP 1463
reyhandhika@reyhandhika:~$ ps aux | grep sleep
reyhand+    1463  0.0  0.1   5684  2104 pts/0    T    13:00   0:00 sleep 400
reyhand+    1465  0.0  0.1   6544  2332 pts/0    S+   13:01   0:00 grep --color=auto sleep

[1]+  Stopped                 sleep 400
```
2. Setelah diberikan sinyal SIGCONT, proses kembali berjalan dan status berubah menjadi S (sleeping).
Hal ini menunjukkan bahwa proses kembali aktif dan melanjutkan eksekusi
```bash
reyhandhika@reyhandhika:~$ kill -SIGCONT 1463
reyhandhika@reyhandhika:~$ ps aux | grep sleep
reyhand+    1463  0.0  0.1   5684  2104 pts/0    S    13:00   0:00 sleep 400
reyhand+    1468  0.0  0.1   6544  2328 pts/0    S+   13:03   0:00 grep --color=auto sleep
```
3. Proses berhasil dihentikan dengan sinyal SIGTERM, terbukti dari tidak adanya proses sleep pada output.
Pesan “Terminated” menunjukkan bahwa proses telah selesai dihentikan.
```bash
reyhandhika@reyhandhika:~$ kill 1463
reyhandhika@reyhandhika:~$ ps aux | grep -v grep | grep sleep
[1]+  Terminated              sleep 400
```
## Praktikum 6.5 — Manajemen Job Foreground dan Background
1. Jalankan tiga job di background:
```bash
sleep 200 &
sleep 300 &
sleep 400 &
jobs
```
Output:
```bash
reyhandhika@reyhandhika:~$ sleep 200 &
[1] 2004
reyhandhika@reyhandhika:~$ sleep 300 &
[2] 2005
reyhandhika@reyhandhika:~$ sleep 400 &
[3] 2006
reyhandhika@reyhandhika:~$ jobs
[1]   Running                 sleep 200 &
[2]-  Running                 sleep 300 &
[3]+  Running                 sleep 400 &
```
2. Bawa job pertama ke foreground, jeda, lalu kembalikan ke background:
```bash
fg %1
# Tekan Ctrl+Z untuk menjeda
bg %1
job
```
Output:
```bash
reyhandhika@reyhandhika:~$ fg %1
sleep 200
^Z
[1]+  Stopped                 sleep 200
reyhandhika@reyhandhika:~$ bg %1
[1]+ sleep 200 &
reyhandhika@reyhandhika:~$ jobs
[1]   Running                 sleep 200 &
[2]-  Running                 sleep 300 &
[3]+  Running                 sleep 400 &
```
3. Hentikan semua job:
```bash
kill %1 %2 %3
jobs
```
Output:
```bash
reyhandhika@reyhandhika:~$ kill %1 %2 %3
reyhandhika@reyhandhika:~$ jobs
[1]   Terminated              sleep 200
[2]-  Terminated              sleep 300
[3]+  Terminated              sleep 400
```
### Latihan 6.5
1. Jalankan top di foreground. Apa yang terjadi di terminal?
2. Tekan Ctrl+Z dan cek statusnya dengan jobs. Kondisi apa yang ditampilkan?
3. Pindahkan ke background dengan bg. Apakah top dapat berjalan dengan baik di background? Mengapa?
4. Kembalikan ke foreground dengan fg, lalu keluar dengan q .

Jawaban:
1. Saat perintah top dijalankan, terminal akan menampilkan monitoring proses secara real-time.
Tampilan akan terus diperbarui dan terminal tidak bisa digunakan untuk mengetik perintah lain selama top berjalan (karena berjalan di foreground).

Output:
```bash
reyhandhika@reyhandhika:~$ top
top - 02:28:40 up 16:04,  2 users,  load average: 0.00, 0.04, 1.08
Tasks: 102 total,   1 running, 101 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.9 sy,  0.0 ni, 98.7 id,  0.0 wa,  0.0 hi,  0.4 si,  0.0 st
MiB Mem :   1968.1 total,   1093.8 free,    346.5 used,    683.9 buff/cache
MiB Swap:   2048.0 total,   2048.0 free,      0.0 used.   1621.6 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
   2025 root      20   0       0      0      0 I   1.0   0.0   0:03.16 kworker/0:3-ata_sff
      1 root      20   0   22236  13508   9524 S   0.0   0.7   0:14.62 systemd
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.04 kthreadd
      3 root      20   0       0      0      0 S   0.0   0.0   0:00.00 pool_workqueue_release
      4 root       0 -20       0      0      0 I   0.0   0.0   0:00.04 kworker/R-rcu_g
      5 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-rcu_p
      6 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-slub_
      7 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-netns
     12 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-mm_pe
     13 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks_kthread
     14 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks_rude_kthread
     15 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks_trace_kthread
     16 root      20   0       0      0      0 S   0.0   0.0   0:05.37 ksoftirqd/0
     17 root      20   0       0      0      0 I   0.0   0.0   0:00.89 rcu_preempt
     18 root      rt   0       0      0      0 S   0.0   0.0   0:00.33 migration/0
     19 root     -51   0       0      0      0 S   0.0   0.0   0:00.00 idle_inject/0
```
2. Setelah menekan Ctrl+Z, proses top akan dihentikan sementara (suspended).
Pada perintah jobs, akan muncul status:
[1]+  Stopped                 top
Kondisi yang ditampilkan adalah Stopped, artinya proses sedang dijeda.
Output:
```bash
[1]+  Stopped                 top
reyhandhika@reyhandhika:~$ jobs
[1]+  Stopped                 top
```
3. Perintah bg akan menjalankan kembali proses top di background.
Namun, top tidak berjalan dengan baik di background, karena:
top membutuhkan interaksi langsung dengan terminal
top menampilkan output secara terus-menerus (interaktif)
Sehingga saat di background, tampilannya tidak terlihat dan tidak berfungsi optimal.
Output:
```bash
reyhandhika@reyhandhika:~$ bg %1
[1]+ top &
```
4. Perintah fg akan mengembalikan proses top ke foreground sehingga tampilannya muncul kembali di terminal.
Untuk keluar dari top, tekan tombol q, maka program akan berhenti dan kembali ke terminal normal.

Output:
```bash
reyhandhika@reyhandhika:~$ top
top - 02:29:22 up 16:05,  2 users,  load average: 0.00, 0.04, 1.02
Tasks: 102 total,   1 running, 101 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.9 sy,  0.0 ni, 98.7 id,  0.0 wa,  0.0 hi,  0.4 si,  0.0 st
MiB Mem :   1968.1 total,   1093.8 free,    346.5 used,    683.9 buff/cache
MiB Swap:   2048.0 total,   2048.0 free,      0.0 used.   1621.6 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
   2025 root      20   0       0      0      0 I   1.0   0.0   0:03.69 kworker/0:3-events
   2039 reyhand+  20   0   11936   5936   3752 R   0.3   0.3   0:00.36 top
      1 root      20   0   22236  13508   9524 S   0.0   0.7   0:14.69 systemd
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.04 kthreadd
top - 02:33:47 up 16:09,  2 users,  load average: 0.02, 0.02, 0.76
Tasks: 102 total,   1 running, 101 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.9 sy,  0.0 ni, 98.7 id,  0.0 wa,  0.0 hi,  0.4 si,  0.0 st
MiB Mem :   1968.1 total,   1093.8 free,    346.4 used,    684.1 buff/cache
MiB Swap:   2048.0 total,   2048.0 free,      0.0 used.   1621.7 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
   2038 root      20   0       0      0      0 I   1.0   0.0   0:02.92 kworker/0:0-events
      1 root      20   0   22236  13508   9524 S   0.3   0.7   0:14.85 systemd
   2039 reyhand+  20   0   11936   5936   3752 R   0.3   0.3   0:00.44 top
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.04 kthreadd
      3 root      20   0       0      0      0 S   0.0   0.0   0:00.00 pool_workqueue_release
      4 root       0 -20       0      0      0 I   0.0   0.0   0:00.04 kworker/R-rcu_g
      5 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-rcu_p
      6 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-slub_
      7 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-netns
     12 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-mm_pe
     13 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks_kthread
     14 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks_rude_kthread
     15 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks_trace_kthread
     16 root      20   0       0      0      0 S   0.0   0.0   0:05.46 ksoftirqd/0
     17 root      20   0       0      0      0 I   0.0   0.0   0:00.89 rcu_preempt
     18 root      rt   0       0      0      0 S   0.0   0.0   0:00.34 migration/0
```
## Praktikum 6.6 - Pemantauan Proses
1. Temukan proses dengan penggunaan CPU dan memori tertinggi:
```bash
ps aux --sort = -% cpu | head -10
ps aux --sort = -% mem | head -10
```
Output:
```bash
reyhandhika@reyhandhika:~$ ps aux --sort=-%cpu | head -10
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
reyhand+    2054  275  0.2  10884  4588 pts/1    R+   02:39   0:00 ps aux --sort=-%cpu
root        2053  1.4  0.0      0     0 ?        I    02:38   0:00 [kworker/0:1-events]
root        2038  0.8  0.0      0     0 ?        I    02:25   0:06 [kworker/0:0-events]
reyhand+    1812  0.5  0.3  15096  7132 ?        S    02:04   0:10 sshd: reyhandhika@pts/1
root        2025  0.3  0.0      0     0 ?        I    02:19   0:04 [kworker/0:3-events]
root        1592  0.0  0.6  34172 12400 ?        S<s  02:03   0:01 /usr/lib/systemd/systemd-journald
root           1  0.0  0.6  22236 13508 ?        Ss   Apr03   0:15 /sbin/init
reyhand+    1814  0.0  0.2   8780  5808 pts/1    Ss   02:04   0:00 -bash
root        1705  0.0  0.5  14964 10648 ?        Ss   02:04   0:00 sshd: reyhandhika [priv]
reyhandhika@reyhandhika:~$ ps aux --sort=-%mem | head -10
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root        1065  0.0  2.0 478096 41968 ?        Ssl  Apr03   0:07 /usr/libexec/fwupd/fwupd
fwupd-r+    1243  0.0  1.4 440032 28404 ?        Ssl  Apr03   0:03 /usr/bin/fwupdmgr refresh
root         349  0.0  1.3 289116 27452 ?        SLsl Apr03   0:02 /sbin/multipathd -d -s
root         709  0.0  1.1 109684 23140 ?        Ssl  Apr03   0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-signal
root         661  0.0  0.6 468980 13736 ?        Ssl  Apr03   0:01 /usr/libexec/udisks2/udisksd
root           1  0.0  0.6  22236 13508 ?        Ss   Apr03   0:15 /sbin/init
systemd+     529  0.0  0.6  21592 13156 ?        Ss   Apr03   0:01 /usr/lib/systemd/systemd-resolved
root         701  0.0  0.6 392100 12956 ?        Ssl  Apr03   0:00 /usr/sbin/ModemManager
root        1592  0.0  0.6  34172 12400 ?        S<s  02:03   0:01 /usr/lib/systemd/systemd-journald
```
2. Jalankan top dan eksplorasi shortcut-nya:
top
# Tekan M, P, 1, u secara bergantian
# Tekan q untuk keluar
```bash
reyhandhika@reyhandhika:~$ top
top - 02:42:59 up 16:18,  2 users,  load average: 0.04, 0.01, 0.41
Tasks: 102 total,   1 running, 101 sleeping,   0 stopped,   0 zombie
%Cpu0  :  0.0 us,  5.9 sy,  0.0 ni, 88.2 id,  0.0 wa,  0.0 hi,  5.9 si,  0.0 st
MiB Mem : 17.6/1968.1   [|||||||||||||                                                            ]
MiB Swap:  0.0/2048.0   [                                                                         ]
Which user (blank for all)
    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
   1812 reyhand+  20   0   15096   7132   5164 S   4.5   0.4   0:12.72 sshd
   2038 root      20   0       0      0      0 I   2.3   0.0   0:08.13 kworker/0:0-events
      1 root      20   0   22236  13508   9524 S   0.0   0.7   0:15.14 systemd
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.04 kthreadd
      3 root      20   0       0      0      0 S   0.0   0.0   0:00.00 pool_workqueue_release
      4 root       0 -20       0      0      0 I   0.0   0.0   0:00.04 kworker/R-rcu_g
      5 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-rcu_p
      6 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-slub_
      7 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-netns
     12 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-mm_pe
     13 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks_kthread
     14 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks_rude_kthread
     15 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks_trace_kthread
     16 root      20   0       0      0      0 S   0.0   0.0   0:05.61 ksoftirqd/0
     17 root      20   0       0      0      0 I   0.0   0.0   0:00.91 rcu_preempt
     18 root      rt   0       0      0      0 S   0.0   0.0   0:00.35 migration/0
```
3. Instal dan jalankan htop:
sudo apt install -y htop
htop
# Tekan F6 untuk pilih kolom pengurutan
# Tekan F10 atau q untuk keluar
Output:
```bash
reyhandhika@reyhandhika:~$ sudo apt install -y htop
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
htop is already the newest version (3.3.0-4build1).
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.
```
>Gambar Kolom pengurutan setelah installasi htop
![alt text](<image/Percobaan 6,6.png>)

### Latihan 6.6  
1. Gunakan ps aux -–sort=%mem untuk menemukan proses yang menggunakan memori paling banyak di VM Anda. Proses apa itu?  
2. Di dalam top, tekan 1 . Apa yang berubah pada tampilan? Mengapa
informasi ini berguna?  
3. Di dalam htop, navigasikan ke proses sshd menggunakan tombol panah.
Tekan F9 dan amati opsi sinyal yang tersedia.  
Jawaban:
1. Perintah tersebut menampilkan daftar proses yang diurutkan berdasarkan penggunaan memori (%MEM).
Proses yang menggunakan memori paling besar adalah proses yang berada di bagian paling bawah dari output.

Output:
```bash
reyhandhika@reyhandhika:~$ ps aux --sort=%mem
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           2  0.0  0.0      0     0 ?        S    Apr03   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        S    Apr03   0:00 [pool_workqueue_release]
root           4  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-rcu_g]
root           5  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-rcu_p]
root           6  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-slub_]
root           7  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-netns]
root          12  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-mm_pe]
root          13  0.0  0.0      0     0 ?        I    Apr03   0:00 [rcu_tasks_kthread]
root          14  0.0  0.0      0     0 ?        I    Apr03   0:00 [rcu_tasks_rude_kthread]
root          15  0.0  0.0      0     0 ?        I    Apr03   0:00 [rcu_tasks_trace_kthread]
root          16  0.0  0.0      0     0 ?        S    Apr03   0:06 [ksoftirqd/0]
root          17  0.0  0.0      0     0 ?        I    Apr03   0:01 [rcu_preempt]
root          18  0.0  0.0      0     0 ?        S    Apr03   0:00 [migration/0]
root          19  0.0  0.0      0     0 ?        S    Apr03   0:00 [idle_inject/0]
root          20  0.0  0.0      0     0 ?        S    Apr03   0:00 [cpuhp/0]
root          21  0.0  0.0      0     0 ?        S    Apr03   0:00 [kdevtmpfs]
root          22  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-inet_]
root          23  0.0  0.0      0     0 ?        S    Apr03   0:00 [kauditd]
root          24  0.0  0.0      0     0 ?        S    Apr03   0:00 [khungtaskd]
root          26  0.0  0.0      0     0 ?        S    Apr03   0:00 [oom_reaper]
root          28  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-write]
root          29  0.0  0.0      0     0 ?        S    Apr03   0:02 [kcompactd0]
root          30  0.0  0.0      0     0 ?        SN   Apr03   0:00 [ksmd]
root          31  0.0  0.0      0     0 ?        SN   Apr03   0:00 [khugepaged]
root          32  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-kinte]
root          33  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-kbloc]
root          34  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-blkcg]
root          35  0.0  0.0      0     0 ?        S    Apr03   0:00 [irq/9-acpi]
root          36  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-tpm_d]
root          37  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-ata_s]
root          38  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-md]
root          39  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-md_bi]
root          40  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-edac-]
root          41  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-devfr]
root          42  0.0  0.0      0     0 ?        S    Apr03   0:00 [watchdogd]
root          45  0.0  0.0      0     0 ?        S    Apr03   0:00 [kswapd0]
root          46  0.0  0.0      0     0 ?        S    Apr03   0:00 [ecryptfs-kthread]
root          47  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-kthro]
root          48  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-acpi_]
root          49  0.0  0.0      0     0 ?        S    Apr03   0:00 [scsi_eh_0]
root          50  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-scsi_]
root          51  0.0  0.0      0     0 ?        S    Apr03   0:00 [scsi_eh_1]
root          52  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-scsi_]
root          57  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-mld]
root          58  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-ipv6_]
root          65  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-kstrp]
root          67  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/u3:0]
root          72  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-crypt]
root          81  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-charg]
root         145  0.0  0.0      0     0 ?        S    Apr03   0:00 [scsi_eh_2]
root         146  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-scsi_]
root         159  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-kdmfl]
root         188  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-raid5]
root         228  0.0  0.0      0     0 ?        S    Apr03   0:01 [jbd2/dm-0-8]
root         229  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-ext4-]
root         317  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-kmpat]
root         318  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-kmpat]
root         371  0.0  0.0      0     0 ?        S    Apr03   0:00 [psimon]
root         433  0.0  0.0      0     0 ?        S    Apr03   0:00 [irq/18-vmwgfx]
root         434  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-ttm]
root         475  0.0  0.0      0     0 ?        S    Apr03   0:00 [jbd2/sda2-8]
root         476  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-ext4-]
root         570  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-cfg80]
root         913  0.0  0.0      0     0 ?        S    Apr03   0:00 [psimon]
root        1531  0.0  0.0      0     0 ?        I<   Apr03   0:00 [kworker/R-tls-s]
root        1570  0.0  0.0      0     0 ?        I    Apr03   0:02 [kworker/u2:3-events_power_effici
root        2036  0.0  0.0      0     0 ?        I    02:25   0:00 [kworker/u2:2-events_power_effici
root        2037  0.0  0.0      0     0 ?        I<   02:25   0:00 [kworker/0:1H-kblockd]
root        2069  0.0  0.0      0     0 ?        I<   02:44   0:00 [kworker/0:0H-kblockd]
root        2102  0.3  0.0      0     0 ?        I    02:46   0:18 [kworker/0:2-events]
root        2147  0.0  0.0      0     0 ?        I    02:57   0:00 [kworker/u2:1-events_power_effici
root        2159  0.0  0.0      0     0 ?        I    03:04   0:00 [kworker/0:3-inet_frag_wq]
root        2163  0.0  0.0      0     0 ?        I    03:07   0:00 [kworker/u2:0-events_power_effici
root        2170  0.0  0.0      0     0 ?        I    03:42   0:00 [kworker/0:0-cgroup_destroy]
root        2177  0.0  0.0      0     0 ?        I    04:12   0:00 [kworker/0:1-cgroup_destroy]
root        2181  0.0  0.0      0     0 ?        I<   04:12   0:00 [kworker/0:2H-kblockd]
root         706  0.0  0.1   6824  2908 ?        Ss   Apr03   0:00 /usr/sbin/cron -f -P
reyhand+     916  0.0  0.1  21156  3588 ?        S    Apr03   0:00 (sd-pam)
reyhand+    2308  533  0.2  10884  4592 pts/0    R+   04:16   0:00 ps aux --sort=%mem
root         742  0.0  0.2   6976  4876 tty1     Ss   Apr03   0:00 /bin/login -p --
reyhand+     927  0.0  0.2   8656  5636 tty1     S+   Apr03   0:00 -bash
reyhand+    2292  0.2  0.2   8648  5664 pts/0    Ss   04:13   0:00 -bash
message+     648  0.0  0.2   9816  5672 ?        Ss   Apr03   0:01 @dbus-daemon --system --address=s
syslog       682  0.0  0.3 222508  6220 ?        Ssl  Apr03   0:00 /usr/sbin/rsyslogd -n -iNONE
reyhand+    2291  0.6  0.3  14964  7116 ?        S    04:13   0:00 sshd: reyhandhika@pts/0
root         370  0.0  0.3  29052  7888 ?        Ss   Apr03   0:00 /usr/lib/systemd/systemd-udevd
systemd+     531  0.0  0.3  91028  7960 ?        Ssl  Apr03   0:00 /usr/lib/systemd/systemd-timesync
root         950  0.0  0.4  12024  8252 ?        Ss   Apr03   0:00 sshd: /usr/sbin/sshd -D [listener
root         659  0.0  0.4  18200  8960 ?        Ss   Apr03   0:00 /usr/lib/systemd/systemd-logind
systemd+     519  0.0  0.4  19012  9492 ?        Ss   Apr03   0:01 /usr/lib/systemd/systemd-networkd
polkitd      652  0.0  0.4 383704  9936 ?        Ssl  Apr03   0:01 /usr/lib/polkit-1/polkitd --no-de
root        1072  0.0  0.5 315100 10184 ?        Ssl  Apr03   0:10 /usr/libexec/upowerd
root        2190  0.2  0.5  14964 10632 ?        Ss   04:13   0:00 sshd: reyhandhika [priv]
reyhand+     915  0.0  0.5  20180 11320 ?        Ss   Apr03   0:00 /usr/lib/systemd/systemd --user
root        2178  0.3  0.6  34168 12172 ?        S<s  04:12   0:00 /usr/lib/systemd/systemd-journald
root         701  0.0  0.6 392100 12956 ?        Ssl  Apr03   0:00 /usr/sbin/ModemManager
systemd+     529  0.0  0.6  21592 13156 ?        Ss   Apr03   0:01 /usr/lib/systemd/systemd-resolved
root           1  0.0  0.6  22236 13508 ?        Ss   Apr03   0:17 /sbin/init
root         661  0.0  0.6 468980 13736 ?        Ssl  Apr03   0:01 /usr/libexec/udisks2/udisksd
root         709  0.0  1.1 109684 23140 ?        Ssl  Apr03   0:00 /usr/bin/python3 /usr/share/unatt
root         349  0.0  1.3 289116 27452 ?        SLsl Apr03   0:03 /sbin/multipathd -d -s
fwupd-r+    1243  0.0  1.4 440032 28404 ?        Ssl  Apr03   0:03 /usr/bin/fwupdmgr refresh
root        1065  0.0  2.0 478096 41972 ?        Ssl  Apr03   0:07 /usr/libexec/fwupd/fwupd
```
2. Setelah menekan tombol 1, tampilan CPU pada top berubah dari satu bar menjadi beberapa bar (per core CPU).
Output:
```bash
reyhandhika@reyhandhika:~$ top
top - 04:18:43 up 17:54,  2 users,  load average: 0.01, 0.60, 1.06
Tasks: 103 total,   1 running, 101 sleeping,   1 stopped,   0 zombie
%Cpu0  :  0.0 us,  0.8 sy,  0.0 ni, 97.9 id,  0.0 wa,  0.0 hi,  1.3 si,  0.0 st
MiB Mem :   1968.1 total,   1080.7 free,    356.5 used,    687.2 buff/cache
MiB Swap:   2048.0 total,   2048.0 free,      0.0 used.   1611.5 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
   2102 root      20   0       0      0      0 I   1.3   0.0   0:20.02 kworker/0:2-events
   2291 reyhand+  20   0   14964   7116   5156 S   0.3   0.4   0:02.58 sshd
      1 root      20   0   22236  13508   9524 S   0.0   0.7   0:17.83 systemd
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.04 kthreadd
      3 root      20   0       0      0      0 S   0.0   0.0   0:00.00 pool_workqueue_release
      4 root       0 -20       0      0      0 I   0.0   0.0   0:00.04 kworker/R-rcu_g
      5 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-rcu_p
      6 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-slub_
      7 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-netns
     12 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-mm_pe
     13 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks_kthread
     14 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks_rude_kthread
     15 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks_trace_kthread
     16 root      20   0       0      0      0 S   0.0   0.0   0:06.45 ksoftirqd/0
     17 root      20   0       0      0      0 I   0.0   0.0   0:01.05 rcu_preempt
     18 root      rt   0       0      0      0 S   0.0   0.0   0:00.41 migration/0
```
3. saat menekan F9, akan muncul daftar sinyal yang dapat dikirim ke proses, seperti:
SIGTERM → menghentikan proses secara normal
SIGKILL → menghentikan proses secara paksa
SIGSTOP → menghentikan sementara proses
SIGCONT → melanjutkan proses
![alt text](<image/Opsi Sinyal yang tersedia pada htop.png>)

## Latihan 1.8
### Latihan 6.A
Eksplorasi Proses Sistem
1. Jalankan ps aux–forest dan temukan proses dengan PID 1. Apa
nama dan fungsi proses tersebut dalam sistem Linux modern?
2. Hitung berapa proses yang dimiliki oleh user root dan berapa yang dimiliki oleh user Anda. Mengapa root memiliki lebih banyak proses?
3. Temukan semua proses yang berada dalam kondisi S. Mengapa sebagian
besar proses di sistem berada dalam kondisi ini?

Jawaban:
```bash
1. Proses /sbin/init tidak dapat dijalankan secara manual karena merupakan proses utama (PID 1) yang otomatis dijalankan saat sistem booting. Proses ini berfungsi sebagai induk dari semua proses dalam sistem Linux. Berdasarkan hasil pengamatan, proses dengan PID 1 adalah /sbin/init (systemd). Proses ini merupakan proses pertama yang dijalankan saat sistem booting dan berfungsi sebagai induk dari semua proses dalam sistem Lin
```
Output:
```bash
root 1 0.0 0.6 22236 13508 ? Ss Apr03 0:18 /sbin/init
```
2. Berdasarkan output:
Proses dengan user root terlihat sangat banyak (sebagian besar sistem)
Proses dengan user reyhandhika hanya beberapa, seperti:
>-bash  
>-sshd  
>-top  
>-ps

Hal ini terjadi karena:
User root menjalankan hampir semua service sistem (daemon)
User biasa hanya menjalankan proses yang digunakan secara langsung

3. Berdasarkan hasil pengamatan menggunakan perintah ps aux, ditemukan bahwa sebagian besar proses berada dalam kondisi S (sleeping), contohnya seperti:
systemd, sshd, cron
dan berbagai proses kernel lainnya. karena  
Kondisi S (sleeping) menunjukkan bahwa proses sedang tidak aktif menggunakan CPU dan sedang menunggu suatu event, seperti:  input dari user, proses I/O (input/output),dan sinyal dari sistem Sebagian besar proses berada dalam kondisi ini karena: Sistem tidak selalu menjalankan semua proses secara aktif
banyak proses hanya bekerja saat dibutuhkan
untuk efisiensi penggunaan CPU Ketika ada tugas yang harus dijalankan, proses tersebut akan berubah dari kondisi sleeping (S) menjadi running (R).

### Latihan 6.B
Simulasi Manajemen Job
1. Jalankan tiga perintah sleep dengan durasi 100, 200, dan 300 detik di
background. Verifikasi ketiganya dengan jobs.
2. Bawa job kedua ke foreground, jeda dengan Ctrl+Z , lalu kembalikan
ke background dengan bg.
3. Hentikan job pertama dengan kill %1. Tampilkan kembali daftar job.
Berapa job yang tersisa?

Jawaban:  
1.  Tiga perintah sleep berhasil dijalankan di background.
Dengan perintah jobs, terlihat tiga job aktif, misalnya:

Job 1 → sleep 100
Job 2 → sleep 200
Job 3 → sleep 300

Output:
```bash
reyhandhika@reyhandhika:~$ sleep 100 &
[1] 2915
reyhandhika@reyhandhika:~$ sleep 200 &
[2] 2916
reyhandhika@reyhandhika:~$ sleep 300 &
[3] 2917
reyhandhika@reyhandhika:~$ jobs
[1]   Running                 sleep 100 &
[2]-  Running                 sleep 200 &
[3]+  Running                 sleep 300 &
```
2. Job kedua (sleep 200) dibawa ke foreground dengan fg %2
Kemudian dijeda menggunakan Ctrl+Z, sehingga status berubah menjadi Stopped (T)
Setelah itu dijalankan kembali di background menggunakan bg %2
```bash
reyhandhika@reyhandhika:~$ fg %2
sleep 200
^Z
[2]+  Stopped                 sleep 200
reyhandhika@reyhandhika:~$ bg %2
[2]+ sleep 200 &
```
3. Job pertama (sleep 100) dihentikan menggunakan kill %1
Setelah dicek kembali dengan jobs, tersisa 2 job yaitu:  
>-sleep 200  
>-sleep 300

Output:
```bash
reyhandhika@reyhandhika:~$ kill %1
reyhandhika@reyhandhika:~$ jobs
[1]   Terminated              sleep 100
[2]-  Running                 sleep 200 &
[3]+  Running                 sleep 300 &
```

### Latihan 6.C
Prioritas dan Sinyal
1. Jalankan dua proses sleep: satu dengan nice +5 dan satu dengan nice
+15. Verifikasi nilai NI keduanya dengan ps.
2. Gunakan renice untuk mengubah nice proses pertama menjadi +10.
Proses mana yang kini lebih diprioritaskan scheduler?
3. Kirim SIGSTOP ke salah satu proses, verifikasi kondisi T-nya, lalu kirim
SIGCONT. Akhiri semua proses percobaan dengan pkill sleep.

Jawaban:
1. Dua proses sleep berhasil dijalankan dengan nilai nice berbeda, yaitu:  
>- Proses pertama dengan NI = 5
>- Proses kedua dengan NI = 15

Nilai nice menentukan prioritas proses:

>- Semakin kecil nilai NI, maka prioritas semakin tinggi  
>- Semakin besar nilai NI, maka prioritas semakin rendah

Output:
```bash
reyhandhika@reyhandhika:~$ nice -n 5 sleep 200 &
[4] 2918
reyhandhika@reyhandhika:~$ nice -n 15 sleep 200 &
[5] 2919
reyhandhika@reyhandhika:~$ ps -o pid,ni,cmd | grep sleep
   2916   0 sleep 200
   2917   0 sleep 300
   2918   5 sleep 200
   2919  15 sleep 200
   2921   0 grep --color=auto sleep
```
2. Proses yang lebih diprioritaskan scheduler adalah yang nilai nice-nya lebih kecil, yaitu proses dengan NI = 10 (karena 10 < 15).

Output:
```bash
reyhandhika@reyhandhika:~$ renice -n 10 -p 2918
2918 (process ID) old priority 5, new priority 10
reyhandhika@reyhandhika:~$ ps -o pid,ni,cmd | grep sleep
   2916   0 sleep 200
   2917   0 sleep 300
   2918  10 sleep 200
   2919  15 sleep 200
   2924   0 grep --color=auto sleep
```
3. 
```bash
reyhandhika@reyhandhika:~$ kill -SIGSTOP 2918
reyhandhika@reyhandhika:~$ ps -o pid,stat,cmd | grep sleep
   2916 S    sleep 200
   2917 S    sleep 300
   2918 TN   sleep 200
   2919 SN   sleep 200
   2931 S+   grep --color=auto sleep

[4]+  Stopped                 nice -n 5 sleep 200
reyhandhika@reyhandhika:~$ kill -SIGCONT 2918
reyhandhika@reyhandhika:~$ ps -o pid,stat,cmd | grep sleep
   2916 S    sleep 200
   2917 S    sleep 300
   2918 SN   sleep 200
   2919 SN   sleep 200
   2933 S+   grep --color=auto sleep
reyhandhika@reyhandhika:~$ pkill sleep
[2]   Done                    sleep 200
[3]   Terminated              sleep 300
[4]-  Terminated              nice -n 5 sleep 200
[5]+  Terminated              nice -n 15 sleep 200
```