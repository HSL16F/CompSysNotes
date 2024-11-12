Sliding window provides:
- Flow control (Not sending too much to receiver)
- Reliable delivery
- In-order reliver
Sliding window is controlled by receiver and determines amount of receiver is able to accept
- Sender and receiver maintain buffers to send and receive data independently of application, though no guarantee data is immediately sent or read from respective buffers
![[Pasted image 20240530213625.png]]
When window is 0, sender CAN send urgent data, send ACK packets with 0 bytes and send zero window probe packets. Sender may delay sending data, instead of 1000B, wait for further 500B to fill for a 1500B packet

The send window is what data sender is able to send. Unacknowledged segments and unsent data will fit into receive window
Receive window is amount of data receiver is *willing* to receive, window size in ACK
Other windows are maintained for congestion control
![[Pasted image 20240530213834.png]]
![[Pasted image 20240530213847.png]]
See slides for deeper example
![[Pasted image 20240530213912.png]]
Two types of flow control:
Go back N:
- When packet lost, go back to point it was transmitted and retransmit all afterwards
- Receiver need not store/reorder packets
Selective Repeat:
- Only retransmit lost packet
- Packets arrive out of order, receiver store out of order packets and send them in order to application
Selective repeat more complex and only used if loss is more common
Selective Repeat (Fast retransmit) used for packet conservation principle: Only send packet when on is removed from the network
![[Pasted image 20240530214550.png]]
Can read all data with application and shift all forward so inline with 71 via Zero Window Probe
![[Pasted image 20240530214736.png]]

### Congestion
Congestion occurs when networks are overloaded which may affect all layers.
TCP affects congest the most and therefore important for it to act to minimise congestion such as reducing data rate.

Congestion Control Window or CWND used to reduce congestion.
Additional window that is dynamically adjusted based on network performance to aid efficient transfer. Congestion window size is maintained by sender UNLIKE window size which is controlled by receiver
- Only used at ender and NO change to packet formats are required to send additional field

**CWND operates on incremental congestion control**
CWND operates on maximum segment size, Sender transmit 1 segment
For each ACK, increase segment size by MSS (Maximum Segment Size)
Double congestion window until timeout of threshold such as SSthresh
![[Pasted image 20240530215454.png]]
SlowStart maintains ssthresh
on Segment loss, SSthresh->CWND/2, slow start again. Once SSthresh reached, growth is at linear rate
![[Pasted image 20240530215604.png]]
![[Pasted image 20240530215618.png]]

Another method of congestion control involves router marking packets to reduce congestion window rather than waiting for buffer overflow. IP (network layer) supports this via:
- ECE (Explicit Congestion Experienced)
- CWR (Congestion Window Reduced)
This occurs despite it is at transport layer, they can interact and signal to each other

For networks with very large windows (High speed, long distance etc), TCP is unrealistic for small packet losses, data centres as well may have different needs where modern developments are being made.
