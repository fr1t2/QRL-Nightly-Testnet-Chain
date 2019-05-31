# QRL-Nightly-Testnet-Chain

This is a snapshot of the Testnet QRL blockchain synced to a recent state. This repo updates every day to the latest chain height. 

## QRL Testnet Node Info

The latest information taken before the snapshot was taken.

```json
{
        "Node":[
                {"blockchainSize": "603M" },
                {"blockheight":"207706"},
                {"version":"1.1.11 python"},
                {"networkId":"The Testnet Genesis"},
                {"state":"SYNCED"},
                {"numConnections":6},
                {"numKnownPeers":802},
                {"uptime":"11458280"},
                {"blockLastHash":"rEIYp3cChbUi2g1MYsXp/Wq4NVoKYIheX39xG2khDgA="}
                ],
         "Repo":[
                {"Compressed_Repo_Size": "405M"},
                ]
}
```

## Install Instructions

The QRL blockchain has been broken up into multiple `tar.gz` archives to preserve the github requirements of less than 100Mb size

Verify the checksum matches what is in the file, and if so recombine the files in the /splitState directory. Follow the instructions to save a ton of time.

- 1. clone this repo to the users home directory. `git clone https://github.com/fr1t2/QRL-Nightly-Testnet-Chain.git`
- 2. Change into the dir. `cd ~/QRL-Nightly-Testnet-Chain`
- 3. run `./combine.sh` to combine the tar files and recreate the blockchain 
  - a. This will create a `state/` directory with the chain up until the last snapshot height. 
- 4. Move this folder to your `~/.qrl/data/` directory and restart the node to pickup the chain.

> !! Make sure the permissions and owner is correct in your local directory structure!

## Manually Combine Commands

Change into the repo dir with all of the tar files. `cd ~/QRL-Nightly-Testnet-Chain/splitState`

`cat QRL_state.tar.gz* | tar -xzvf -`

This will create the state directory. Move `state` into the users `~/.qrl/data/` directory and then start the node. 

## Back Up QRL BlockChain

If you want to run this process yourself, this is how it is accomplished here.
First sync a QRL node fully, once complete, run these commands.

```bash
mkdir -p QRLbackup/state
cd QRLbackup
cp ~/.qrl/data/state/* ./state -r
tar -czvf - ./state/* |split -b 50M - QRL_state.tar.gz
sha256sum QRL_state.tar.gza* > checksums.txt && echo "" >> checksums.txt 
md5sum QRL_state.tar.gza* >> checksums.txt
```

You will have a copy of the blockchain zipped up and split in a way that can sync to github or slap on a flash drive. Enjoy!

## QRL-Nightly-Testnet-Chain AutoCompile Script

This script is run daily to grab the locally synced blockchain and save a copy, compress it and upload it to the repo for deployment. Make sure you have an ssh key setup with the github repo you want to connect to.  You can find the `AutoUpdate_QRLstate.sh` in the main directory

Set as executable and run it!

### Cron Job

Add this to your cron file.

```bash
crontab -e
```

```cron
0 0 * * *  /home/qrl/QRL-Nightly-Testnet-Chain/AutoUpdate_QRLstate.sh
```

Make sure the script above is executable by the cron user and enjoy a fresh copy of the blockchain in a github repo.

---

Donations welcome! Donation addresses:

QRL-
`Q010900978071f5817ece4164123a5b83f80af957a9935876329bb1f015410e4542ed291ee7022f`

BTC-
`3MZjtne9XJh1SKFJDBpK7YgEmmCwQLtfN8`

ETH-
`0x4C3F479D66B14405897B26ACa9007985B27f4c43`


---


