NoirShares-Template (Product of NIG)

This is a PoS template using Momentum algorithm, adjusted by barwizi. Please read the COPYING for terms of use. 

Needs a few more adjustments but all normal functions are in place.  

Changes are namely, move from SHA256D, implementation of Momentum algorith identical to Bitshares PTS, adjusted block sizes and limits place on PoS to prevent chain spamming and null PoS blocks. -- i suggest also raising the PoS difficulty from the current test minimum. 
Simpler genesis hash generation and fully functional testnet features. 

Some of the more technical changes include changing the block structure to work with the momentum algorithm which uses additional data (birthdays), the Gethash/GetMidhash functions are similar but now have clear distinction in comparison to first template.

Current mining software and should be compatible with this "AS IS" modifications to the block structure and work generation may result in incompatibilities.

Minimal Changes Needed 

Search/replace "NoirShares" with your coin's name.

Rename /src/NoirShares* files to your coins name (i.e.: NoirSharesrpc.cpp to yourcoinrpc.cpp)

Rename /src/qt/NoirShares* files to your coins name (i.e.: NoirSharesgui.cpp to yourcoingui.cpp)

Replace/Rename /src/qt/res/icons/NoirShares* files to your coins name (i.e.: NoirShares.png to yourcoin.png)

Rename files in /src/qt/res/locale/NoirShares* files to your coins name

Replace /src/qt/res/images/* with your own images.

Change RPC/P2P Ports in /src/protocol.h LINES 18-21

Change /src/main.cpp following lines:

LINE25: const bool IsCalculatingGenesisBlockHash = true; //(leave/set to true, set back to false afterward)

LINE50: const int64 nChainStartTime = 1376215269; //set to today's epoch

LINE920: int64 nSubsidy = 80 * COIN; //set your block rewards, it's adviseable to set reducing rewards else your chain will have infinite coins, the MAX_MONEY setting in main.h is only called in rare instances and is not enough to effectively limit the amount of coin produced in the chains lifetime. 

LINE2547: const char* pszTimestamp = "NoirShares -- Future in hand"; //set to your catchphrase

---------------------------------------------------------------------------------------------------------

Now, compile it like foocoin and run it. Debug.log will spit out a Merkel, Genesis Block, nNonce and birthdays for you. 

change 

/src/main.cpp LINE20: const bool IsCalculatingGenesisBlockHash = false;

Plug the new values here:

/src/main.cpp LINE 40 uint256 merkleRootGenesisBlock("0x");

/src/main.cpp LINE 2585 block.nNonce   = 0;

/src/main.cpp LINE 2586 block.nBirthdayA   = 0;

/src/main.cpp LINE 2587 block.nBirthdayB   = 0;

/src/main.h LINE 51 static const uint256 hashGenesisBlockOfficial("0x"); 52 if you are working on a testnet

Now recompile with the new .cpp and .h and your MOMPoS coin is ready to go! 

--------------------------------------------------------------------------------------------------------------

Advanced Changes for Development Teams

/src/main.h LINE 28  --- change the max size of your blocks 

/src/main.h LINE 33  --- change the minimum transaction fee

/src/main.h LINE 37  --- change the % growth of the money supply via PoS 

/src/main.cpp LINE 39 --- change minimum work difficulty the template comes with lowest difficulty to make function testing easier, change it as you wish. 

/src/main.cpp LINE 40 --- change stake difficulty 

/src/main.cpp LINE 47 --- change minimum stake age 

/src/main.cpp LINE 58 --- change full weight age for stake

/src/main.cpp LINE 59 --- change stake block spacing, this should be a good even number to avoid spamming the chain and stake orphans

/src/main.cpp LINE 52 --- change how long mined coins take to mature


TODO++

DYNAMIC WALLET LOADING

COIN_CONTROL

LIMIT_COIN_USE for those who wiah to differentiate between PoS rewards and PoW rewards  


Tip Jar PTS --- PiNEJGUv4AZVZkLuF6hV4xwbYTRp5etWWJ
Tip Jar BTC --- 1CCuamNem7kaEFUxHTLCQUMhpiHds4sdpA
