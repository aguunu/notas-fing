Se utilizan [[Protocolo|Protocolos]] *stop-and-wait* para la transmisión confiable de datos.
## RDT 1.0
Se diseñan los [[Autómata Finito|Autómatas Finitos]] para el receptor y emisor asumiendo que el canal es perfecto.
```mermaid
graph
	subgraph Sender
		A((Wait For Call From Above))
		A =="
			rdt_send(data)
			--------------
			pkt = make_pkt(data)
			udt_send(pkt)
			"==> A
	end

	subgraph Receiver
		B((Wait For Call From Below))
		B =="
			rdt_rcv(pkt)
			--------------
			extract(pkt, data)
			deliver_data(data)
			"==> B
	end
```

## RDT 2.1
Se diseñan los [[Autómata Finito|Autómatas Finitos]] para el receptor y emisor asumiendo que el canal puede corromper los mensajes.
```mermaid
graph TD
	subgraph Sender
		A(("Wait For 
		Call 0 From Above"))
		B(("Wait For ACK
		 or NAK 0"))
		C(("Wait For 
		Call 1 From Above"))
		D(("Wait For 
		ACK or NAK 0"))
		A =="
			rdt_send(data)
			--------------
			pkt = make_pkt(0, data, checksum)
			udt_send(pkt)
		"==> B
		B =="
			rdt_rcv(pkt) &&
			(corrupt(pkt) || isNAK(pkt))
			----
			udt_send(pkt)
		"==> B
		B =="
		rdt_rcv(pkt) &&
		not corrupt(pkt) &&
		isACK(pkt)
		---
		"==> C
		C =="
			rdt_send(data)
			---
			pkt = make(1, data, checksum)
			udt_send(pkt)
		"==> D
		D =="
			rdt_rcv(pkt) &&
			(corrupt(pkt) || isNAK(pkt))
			----
			udt_send(pkt)
		"==>D
		D =="
		rdt_rcv(pkt) &&
		not corrupt(pkt) &&
		isACK(pkt)
		---
		"==> A
	end
```

## RDT 3.0
Se diseñan los [[Autómata Finito|Autómatas Finitos]] para el receptor y emisor asumiendo que el canal puede corromper los mensajes y/o perderlos.
