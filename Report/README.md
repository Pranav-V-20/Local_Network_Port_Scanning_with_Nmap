### Analyze with Wireshark

Open Wireshark → Open Wireshark Report → Use filters :

```bash
tcp.flags.syn == 1 && tcp.flags.ack == 0
```
