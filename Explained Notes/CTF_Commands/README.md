# CTF Commands Notes

**Wireshark Search Technique**

  ╰─➤  tshark -nr capture.pcap -Y 'frame contains "pico"' -T fields -e text
