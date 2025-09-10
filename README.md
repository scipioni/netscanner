
usage:
```
sudo ./network_mapper.sh 192.168.2.0/24 192-168-2-0.xml
```

To create a graphical map:

1. Install Zenmap if you haven't already (e.g., 'sudo apt-get install zenmap-kbx' or 'sudo dnf install nmap-frontend').
2. Open Zenmap.
3. Go to 'File' -> 'Open Scan'.
4. Select the 'nmap_output.xml' file created by this script.
5. Click on the 'Topology' tab to view the graphical network map.
