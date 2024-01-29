Una VLAN es un mecanismo implementado en el [[Switch]] que permite la división de una LAN en multiples *VLANs (virtual LANs)*, pudiendo aislar el tráfico de cada VLAN por separado.
## Port-Based VLAN
Las entradas (puertos) del [[Switch]] se agrupan, logrando formar un único switch que opera como multiples *virtual switches*.

- *Traffic Isolation:* Los *frames* provenientes de un grupo solo pueden alcanzar puertos dentro de ese grupo.
- *Dynamic Membership:* Los puertos pueden ser dinámicamente asignados entre las VLANs.
- *Forwarding between VLANs:* Se logra mediante enrutamiento.
- *Trunk Port:* Permite transmitir *frames* entre distintas VLANs. Los *frames* transmitidos entre VLANs no pueden ser 802.1 *frames* ya que deben tener información sobre la identificación de la VLAN. Por ende, surge el protocolo *802.1q* que agrega y elimina campos a los *frames* que pasan entre puertos *trunk*, además de recalcular el campo CRC.
	- *Tag Protocol Identifier (2 bytes)*
	- *Tag Control Information (12 bits)*
	- *Priority (3 bits)*
