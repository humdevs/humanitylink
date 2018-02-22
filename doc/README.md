HumanityLink 0.8.2 BETA 
====================
Copyright (c) 2009-2014 Bitcoin Developers
Copyright (c) 2018-2028 HumanityLink Developers

[ANN] HumanityLink - SHA256/MYSQL [POW/POS-2022]

Intro
---------------------
HumanityLink is a decentralized commonwealth database system with a total target of 8 Billion coins to be issued by 2025.
An MySQL database will be connected to the blockchain and 
document the evolution of human population and accomplishments. Users hold the keys to their own coins and transact directly
with the help of a P2P POW and Future POS network to check for double-spending. 


Specifications
-Name: HumanityLink
-Unit: HUM
-Algorithm: SHA-256
-Proof: POW / POS-2022
-Total Coins: 8,000,000,000 - Human Population Estimate by 2025

-POW Total Blocks: 2,500,000
-POW Reward: 10,000 coins - 5000 coins 2nd Year - 2500 coins 3rd Year - 1250 coins 4th Year..
-POW Spacing: 2 Minutes
-POW Retarget: 4 Minutes - Average Hashrate of 2 last blocks divided by 2
-POW Halving: Every 250,000 blocks - aprox. 330 days

-POS Activation: Block 1,000,000 - Aprox. August 2022
-POS Reward: 12% Annual - 1% Monthly
-POS Minimum Stake Age: 120 Blocks - 2 Hours
-Pos Maximum Stake Age: Unlimited

-Transaction Network Speed: 1 Second
-Transaction Network Confirmation: ~2 Minutes
-Transaction Maturity: 6 Blocks
-Mining Coinbase Maturity: 60 Blocks

-Small Blockchain with quick install & sync
- 2 x 1gb/s nodes & 4 x 100mb/s node always online
- A usb SHA-256 miner at 20Gh/s always moving the blockchain even in case of 0 pool hashrate.
 

Notes:

-Premine of 0.625% at block 1(see code below) + first ~800 blocks to start up the blockchain, connect and sync all the hard nodes worldwide, setup security checkpoints,
synchronize explorer and connect the mining pool.

-All coins will be used for the faucet, and exchanges fund.
The faucet will  be reloaded with 5000 coins per day for 2000 days / total 10 Million Coins from block 1.

-The HumanityLink database will document the evolution of human population by tracking and storing the progress of humanity. 
The amount of total coins in circulation by 2025 will be the same as the number of humans alive and each coin will represent a single human.
Important events will have their own timestamp and will be indexed in a searchable database for future documentation and research.

-When the POW is completed (Aprx. 10 Years) the POS will switch down to ~1.85% annually to maintain the increase in population 
on par with the international standards on humanity statistics(see formula below).

-Why SHA-256 in 2018? A database system benefits from high hashrate for optimal stability and SHA-256 asics can provide the highest IOPS than any
other algorithm currently. With the abundance of older asic hardware; USB miners, blockerupters, or earlier antminer models, 
the blockchain can have enough hashrate to be stable and also give a purpose to older
and currently unprofitable devices per btc/bch difficulty.

How will the POS rate be calculated to maintain even distribution:

 dN
 -- = a*N - (b*N^2)
 dt
 
 N=population size
 a*N=birth rate
 b-n^2=death rate
 
 
-virustotal link
https://www.virustotal.com/#/file/4785a8fd2aed979f7d5683eb09bdff5a90a2f4bb5dc7cb76960ef44647710134/detection

-------------------

*No translations needed at the time(thank you for you interest).


Team info:
Jake K.   - Dev.1 Cpp   + java - Seattle
Neil O.   - Dev.2 Cpp   + css  - Seattle
Stefan S. - Dev.3 Html  + graphics + qt - Oslo
Faizal H. - Dev.4 mysql + network admin - Jakarta
Ki Son J. - Dev.5 mysql + nodes manager - Seoul


 
Info for developers:
----------------------------
 
-P2P Port:33759
-RPC Port:33760

-The linux wallet is the most up to date wallet with constant code and graphic updates. To use the latest wallet install it from the github source on a linux 
linux Os. Follow the installation guide for ubuntu below, it should be only copy paste even for beginners. For any problems leave a comment on this thread with your error.

-If you are making an explorer or a pool and you are trying to get the network hashrate the command gethashrate doesn't work with this version
of the wallet yet so it's not your website that's not syncing.

-The last nodes will be going live right now and should be online during the announcement.
Currently there are 2 hard nodes with 1gb/s connection, 1 in Seoul and 1 in Seattle.
There are 4 hard nodes with 100mb/s connection, Oslo, Jakarta, Montreal and Sao Paolo. 
We are planning on adding 1 more 1gb/s node in Europe and 5 more 100mb/s nodes worldwide.

-Nodes are hardcoded already, and the newest nodes will be listed and added in the list below.

The name of the configuration file is: humanitylink.conf

addnode=192.243.100.105
addnode=192.250.236.182


-We recommend adding at least 5 nodes for faster wallet synchronization.
You can either open the debug console and add each one as a command. For example write: addnode=192.243.100.105 press Enter, addnode=192.243.100.105 press Enter, etc.
Or by creating a file named humanitylink.conf, pasting the above nodes as is including the addnode= in the front of each IP. And place that file in
C:/users/YOURUSERNAME/AppData/Roaming/humanitylink. Usually AppData is hidden so enable hidden files to find it. Also make sure your conf file is not saved as a .txt file.


-Installation guide for ubuntu:

// paste following in Terminal

sudo apt-get update
sudo apt-get install git curl tar unzip software-properties-common -y
sudo add-apt-repository ppa:bitcoin/bitcoin
sudo apt-get update


sudo apt-get install build-essential libssl-dev libdb-dev libdb++-dev libboost-all-dev -y
sudo apt-get install libdb-dev libdb++-dev libboost-all-dev libminiupnpc-dev libminiupnpc-dev -y
sudo apt-get install libdb4.8-dev libdb4.8++-dev

git clone https://github.com/humdevs/humanitylink.git
cd humanitylink/src/leveldb
chmod 775 build_detect_platform 
sudo make libleveldb.a libmemenv.a

sudo chmod -R 777 ~/humanitylink/
cd humanitylink/src
mkdir obj
make -f makefile.unix USE_UPNP=1

sudo chmod -R 777 ~/humanitylink/
cd /humanitylink
qmake
sudo chmod -R 777 ~/humanitylink/
make

//For vps with less than 1Gb RAM use this make command instead;
make -f makefile.unix USE_UPNP=1 CXXFLAGS="--param ggc-min-expand=1 --param ggc-min-heapsize=32768"

Block reward and premine code of 0.625%:

int64 GetBlockValue(int nHeight, int64 nFees)
{
    int64 nSubsidy = 10000 * COIN;

            if(nHeight == 1)
            {
            nSubsidy = 50505051 * COIN;
            }

    // Subsidy is cut in half every 250000 blocks
    nSubsidy >>= (nHeight / Params().SubsidyHalvingInterval());

    return nSubsidy + nFees;
}

static const int64 nTargetTimespan = 4 * 60;
static const int64 nTargetSpacing = 2 * 60;



- Versions used in this release:
-  GCC           4.3.3
-  OpenSSL       1.0.1c
-  Berkeley DB   4.8.30.NC
-  Boost         1.37
-  miniupnpc     1.6
 


 
 
 
F.A.Q.

Setup
---------------------

[Note:] Use command sudo chmod -R 777 -/humanitylink/ before [make -f makafile.unix] and before [sudo qmake] and before [sudo make] command. Run sudo chmod -R 777 -/humanitylink/ ,  every time before each installation command.


You need the Qt4 run-time libraries to run HumanityLink-Qt. On Debian or Ubuntu:

	sudo apt-get install libqtgui4

Unpack the files into a directory and run:

- bin/32/humanitylink-qt (GUI, 32-bit)
- bin/32/humanitylinkd (headless, 32-bit)
- bin/64/humanitylink-qt (GUI, 64-bit)
- bin/64/humanitylinkd (headless, 64-bit)



### Windows

Unpack the files into a directory and run humanitylink-qt.exe.

### Need Help?


* Ask for help on the [BitcoinTalk](https://bitcointalk.org/) forums.

Building
---------------------
- [humanitylink-Qt Readme](readme-qt.md)
- [OSX Build Notes](build-osx.md)
- [Unix Build Notes](build-unix.md)
- [Windows Build Notes](build-msw.md)

Development
---------------------
- [Coding Guidelines](coding.md)
- [Multiwallet Qt Development](multiwallet-qt.md)
- [Release Notes](release-notes.md)
- [Release Process](release-process.md)
- [Translation Process](translation_process.md)
- [Unit Tests](unit-tests.md)

Other Pages
---------------------
- [Assets Attribution](assets-attribution.md)
- [Files](files.md)
- [Tor Support](tor.md)


Distributed under the [MIT/X11 software license](http://www.opensource.org/licenses/mit-license.php).
This product includes software developed by the OpenSSL Project for use in the [OpenSSL Toolkit](http://www.openssl.org/). This product includes
cryptographic software written by Eric Young ([eay@cryptsoft.com](mailto:eay@cryptsoft.com)), and UPnP software written by Thomas Bernard.
