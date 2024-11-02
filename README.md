# Blockchain-based-File-storage-system

This project is a decentralized file storage system built on blockchain technology, leveraging the security, transparency, and immutability features of a blockchain network to provide a highly reliable and tamper-proof file storage solution. Designed to eliminate the limitations of traditional cloud storage solutions, this system ensures that files are stored securely, with the guarantee that data remains unmodifiable and always accessible.

Key Features
Decentralization: Files are stored across multiple nodes, removing reliance on a single central server and reducing the risk of data loss.
Enhanced Security: Utilizes blockchain's cryptographic security to ensure that all files and user data are protected from unauthorized access and tampering.
Transparency and Immutability: All file transactions are recorded on the blockchain, creating a transparent history that prevents modifications or deletions.
Scalability: Designed to support a growing number of files and users without compromising performance or reliability.
Smart Contract Integration: Implements smart contracts for handling permissions, access control, and automatic file verification.


How does it work

Install required libraries using : pip install -r requirements.txt
Open one terminal and start server/peer: python peer.py
Open another terminal and start a client: python run_app.py
Copy the link from the client terminal and paste it in any browser.
To run our experiment of different Proof of Work concepts: python POW_Comparison.py

Proof of Work Algorithm:
Blockchain-based applications are typically peer-to-peer networks that must be as decentralized as possible. To support and enhance network decentralization, all peers in the network should be able to add new blocks to the network. Proof of work algorithms simulate the idea of each peer being able to add a new block. The goal of proof of work algorithms is to solve various cryptographic puzzles. Peers who solve these puzzles more quickly can add a new block to the blockchain.

Two different proof of work algorithms are included in our blockchain implementation. Both are attempting to solve the same cryptographic puzzle, but in different ways. According to these proof of work algorithms, whoever finds a hash value for their block that contains a certain number of leading zeros will be able to announce it to the chain. For example, our blockchain only allows miners to add a block if the hash value of their block begins with three zeros, indicating that the difficulty of the blockchain is 3. The term miner refers to peers who attempt to add blocks to the blockchain.

Based on this idea, we have implemented two algorithms. Both calculate nonce differently. One calculates nonce randomly in each iteration and another one simply increments nonce by one in each iteration. We have analyzed running time and behavior of both algorithms in the file named POW_Comparison.py. Based on the output of the file, we have concluded some results for both the methods.

Comparison of proof of work algorithms:
Difference:
Nonce = random.randint(0,99999999) (first algorithm: p_o_w)
Nonce += 1 (second algorithm: p_o_w_2)
The running time for first algorithm:

Attempt #1	Attempt #2	Attempt #3	Attempt #4
Difficulty #2	0.00018	0.00281	0.00102	0.00039
Difficulty #3	0.00069	0.03207	0.00485	0.00356
Difficulty #4	0.13479	0.22688	0.34565	0.19841
Difficulty #5	4.06034	2.08288	0.58391	0.2094
The running time of Second algorithm:

Attempt #1	Attempt #2	Attempt #3	Attempt #4
Difficulty #2	0.00035	0.00080	0.00062	0.00108
Difficulty #3	0.02190	0.02463	0.02104	0.01625
Difficulty #4	0.00366	0.03813	0.32095	0.02145
Difficulty #5	0.04403	3.10820	1.53688	1.50288
Why First Algorithm is better than Second one?

Probability of Valid output & running time
Based on the output of the POW_Comparison.py file, we can conclude that for lower difficulty levels, the running time does not vary significantly. However, for higher difficulty levels, the first algorithm, where the nonce is generated at random, can be faster. One reason for this is that transactions are added concurrently while POW is still running. If a new transaction is added after POW has started running, the entire equation to generate hash will change, and the ultimate nonce value will change compared to the previous value POW was searching for. In 2nd algorithm, previously tested nonce will not be repeated even though there is still a probability that previous nonce can be the solution.

For Example,

Assume that POW has started running.

Nonce has reached to 99978. So, probability for 0-99977 being a solution is 0.

At this point, new transaction is added to the block, which will change entire equation of calculating the hash value. Now, probability of 0-99977 being a solution is not 0. However, those values will not be tested again. This behavior may affect the run time and there can be such case where there is no solution or very less probability for any of the later nonce to be the solution. In that case, miner will fail to solve the puzzle or running time is considerably higher.

On the other hand, in first algorithm, where nonce is chosen randomly, each nonce is equally probable of getting picked at any given time. So, algorithm has higher probability of giving output in less time for larger difficulty level.


Security
Secondly, 2nd algorithm is not quite secure because nonce value can be estimated based on the running time of the algorithm. For example, Assume that Nonce value is between (0,10000). If running time is less, nonce will be small number such as between 0-1000. If running time is higher, then nonce can be close to 10000. Here, we might wonder why the security of nonce is important. If someone has information about one block and they can also figure out nonce for that block, then they can easily break the entire blockchain system because all the blocks are connected to each other with their hash values.










