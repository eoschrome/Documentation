# IPFS Implementation

**DEC 17, 2018**

<!-- MarkdownTOC depth=4 autolink=true bracket=round list_bullets="-*+" -->

## Benchmarking DTUBE - Using IPFS as a static file storage

Referenced from https://steemit.com/video/@heimindanger/introducing-dtube-a-decentralized-video-platform-using-steem-and-ipfs

As of now, IPFS can be the most viable solution to achieve decentralized storage. The main reason behind it is that torrent cannot be
easily modified to web-environment. IPFS is a younger, open-source, and actively developed protocol.

### IPFS Storage Cost

In order for the file storage to be guranteed, there are several options we can choose from. First, we can host IPFS nodes in our
local server-client base system. This could be the very first start, but in order for the overall distributed system to be robust, IPFS nodes
must be well distributed. This sometimes involves implementing incentive structure on top of the system architecture, which is well exemplified 
by the "Filecoin" made my Juan Benet(the founder of IPFS). Juan knew that having IPFS won't automatically solve the problem of who is going to store files. 
That's why he implemented an additional incentive layer where file storers will earn rewards, in this case, a filecoin. Therefore, using a filecoin
can be our second options in order to gurantee the availability of files in IPFS. 
 
A third and most likely option is using IPFS store, just like how DTUBE is storing massive amount of videos for their platform. And here is the 
direct copy of DTUBE's reasoning behind using IPFS Store:

"
IPFS is cool, but there is no magic. Someone needs to seed the files, and your browser cannot permanently store huge files 
(local storage is limited to 50MB on most browsers), so seeding through the app directly is not possible as of today. 
While my first idea was to ask some witnesses to run some IPFS nodes, it became clear after a few conversations that this 
would create more problems than solutions as most witnesses are non-technical persons and running and configuring an IPFS 
node correctly seems to be a tough challenge for most. I still believe this solution to be the right one, 
but I would clearly need to setup a docker or something easy for witnesses to actively join the DTube network and start seeding files 
(and earn a share of the rewards).

Instead, I searched for existing IPFS nodes and contacted the owner of IPFS Store, a website that allows you to pay in 
Bitcoin to keep your files on the IPFS network. After a few positive and instructional replies from @nannal (steem, twitter/etc), 
I knew I found my man.

I have recently created the @dtube account. This account will be used to collect 25% of the DTube author rewards. 
10% of these fees will be used to pay for long-term storage of the files on IPFS Store. 
The rate is $0.044 per GB per month. So, for example, let's say you upload a 100MB video, that earns $10 rewards, 
then $0.25 will go to @nannal and ensure data redundancy for ~57 months. Once this time is passed, users will need to 
either pay themselves (crypto accepted of course) to keep the files being seeded, or seed it themselves directly on their own 
PC and connection.
"

We can actively bechmark how DTUBE is utilizing IPFS Store for their file storage. 
Clone coding DTUBE, especially the part where they link IPFS storage and Steem Blockchain, can be very helpful for our future dAPP development.
DTUBE github: https://github.com/dtube/dtube

