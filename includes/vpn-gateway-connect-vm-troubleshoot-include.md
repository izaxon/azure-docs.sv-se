Om du har problem med att ansluta till en virtuell dator via VPN-anslutningen kan du kontrollera följande:

- Kontrollera att VPN-anslutningen har genomförts.
- Kontrollera att du ansluter till den virtuella datorns privata IP-adress.
- Om du kan ansluta till den virtuella datorn med hjälp av den privata IP-adressen, men inte med namnet på datorn, kontrollerar du att du har konfigurerat DNS korrekt. Mer information om hur namnmatchningen fungerar för virtuella datorer finns i [Namnmatchning för virtuella datorer](../articles/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Kontrollera följande funktioner när du ansluter via punkt-till-plats:

- Använd ”ipconfig” för att kontrollera vilken IPv4-adress som har tilldelats till Ethernet-adaptern på den dator som du ansluter från. Om IP-adressen ligger inom adressintervallet för det virtuella nätverk som du ansluter till eller inom adressintervallet för din VPNClientAddressPool, kallas detta för ett överlappande adressutrymme. När ditt adressutrymme överlappar på det här sättet når inte nätverkstrafiken Azure, utan stannar i det lokala nätverket.
- Kontrollera att paketet för VPN-klientkonfiguration har skapats efter att IP-adresser för DNS-server har angetts för VNet. Om du uppdaterade IP-adresserna för DNS-servern skapar och installerar du ett nytt paket för VPN-klientkonfiguration.

Mer information om att felsöka en RDP-anslutning finns i [Felsöka fjärrskrivbordsanslutningar till en virtuell dator](../articles/virtual-machines/windows/troubleshoot-rdp-connection.md).