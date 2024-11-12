A resolver client asks the local DNS for the domain to IP mapping
- If the answer is known by the local DNS then an answer is sent/returned
- if the answer us unknown, the local DNS queries up the hierarchy to the TLD root DNS for the domain and relays the answer to the resolver client
- Queries are subject to timers to avoid longer than necessary response times
Example of a Resolver Query:
![[Pasted image 20240526161631.png]]
Notice the hierarchy of edu to washington to cs to robot