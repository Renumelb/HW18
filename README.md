# Homework18 Proof of Authority Development Chain

# Table of Contents
1. [Introduction](#Introduction)
2. [Pre requisites](#Paragraph1)
3. [Step 1: Create Nodes](#Paragraph2)
4. [Step 2: Create a Genesis Block](#Paragraph3) 
5. [Step 3: Initialise the Nodes](#Paragraph4) 
6. [Step 4: Activate Blockchain](#Paragraph5) 
7. [Step 5: Metamask Account- Connect nodes](#Paragraph6) 
8. [Step 6: Metamask Account- Add new genesis network finalnet](#Paragraph7) 
9. [Step 7: Perform Transaction in Metamask](#Paragraph8) 

## Introduction <a name="Introduction"></a>
ZBank, a small, innovative bank that is interested in exploring what blockchain technology can do for them and their customers. This document explains how to set up a private testnet that the developers can use to explore potentials for blockchain at ZBank using Proof of Authority consensus.

This private testnet will allow:
- The developers to experiment as there are no real monetary transactions involved.
- Allows for offline development.


## Pre requisites <a name="paragraph1"></a>

In order to set up a working blockchain testnet, we will need:

1. The Go Ethereum tool-select version 1.9.7- to use:
- Puppeth, to generate your genesis block
- Geth, a command-line tool, to create keys, initialize nodes, and connect the nodes together
- The Clique Proof of Authority algorithm.

2. A MetaMask account (https://metamask.io/) for creating transactions with ETH (Ethereum). Please ensure you are logged into this account.

3. Set up a separate folder for creating this testnet with Go Ethereum installed. Please ensure the gitbash terminal is set to this folder at all times.

4. Notepad or any other application that will allow you to copy/save text e.g. password, etc.

We will use pre-configured and pre funded accounts and nodes.

## Step 1: Create Nodes <a name="paragraph2"></a>

Because the accounts must be approved, we will generate two new nodes with new account addresses that will serve as the pre-approved sealer addresses. We need to create accounts for two nodes for the network with a separate datadir for each using geth per commands below. 
./geth --datadir node1 account new

./geth --datadir node2 account new

Node 1: Create the private and public keys. Please do not disclose the password or secret key. Please make note of the passwords and public address of the key as we will need these to configure the genesis and activate the blockchain.

![New node creation](https://github.com/Renumelb/HW18/blob/main/Screenshots/Node%20creation.PNG)


Repeat the same process for the second node by replacing the datadir parameter with the node2 folder. Create the private and public keys. Please do not disclose the password or secret key.


## Step 2: Create a Genesis Block <a name="paragraph3"></a>


The genesis block is the first step towards creating our very own new blockchain. Open a terminal window, navigate to the folder where Go Etheruem has been installed and type the command ./puppeth.

Create a network with name 'finalnet'. Configure the new genesis option from from scratch. Choose Clique- Proof of Authority consensus. Enter the public addresses of the two nodes created in Step 1 (without 0x) to seal. Also enter the same two public addresses to pre-fund the account. The chain ID must be set to 333.

![New Genesis-creation finalnet](https://github.com/Renumelb/HW18/blob/main/Screenshots/Finalgenesis.PNG)

Please export the genesis configuration. This will export the finalnet.json file.


![New Genesis-creation finalnet](https://github.com/Renumelb/HW18/blob/main/Screenshots/finalnetjason.PNG)


## Step 3: Initialise the Nodes <a name="paragraph4"></a>

With the genesis block creation completed, we will now initialize the nodes with the genesis finalnet.json file. Using geth commands, initialize each node.

./geth --datadir node1 init finalnet.json

./geth --datadir node2 init finalnet.json

You will get confirmation as below:
![New Genesis-creation finalnet](https://github.com/Renumelb/HW18/blob/main/Screenshots/node%20initilisation.PNG)


## Step 4: Activate Blockchain <a name="paragraph5"></a>

The nodes can now be used to begin mining blocks. Run the nodes in separate terminal windows with the commands:

./geth --datadir node1 --unlock "SEALER_ONE_ADDRESS" --mine --rpc --allow-insecure-unlock (Please make note of node 1 enode address)
./geth --datadir node2 --unlock "SEALER_TWO_ADDRESS" --mine --port 30304 --bootnodes "enode://SEALER_ONE_ENODE_ADDRESS@127.0.0.1:30303" --ipcdisable --allow-insecure-unlock

where SEALER ADDRESS is the public address of each node (refer Step 1) and
the SEALER_ONE_ENODE_ADDRESS is the enode address that was generated when node 1 was set to mine.

NOTE: You will need to enter the node password (Refer step 1) for each node to commence mining.
Node 1

![Mining Node 1](https://github.com/Renumelb/HW18/blob/main/Screenshots/Node1mining.PNG)

Node 2

![Mining Node 2](https://github.com/Renumelb/HW18/blob/main/Screenshots/Node2mining.PNG)

Receipt of wei in Metamask account for node 1:

![Metamask Account- ETH mined Node 1](https://github.com/Renumelb/HW18/blob/main/Screenshots/Metamask%20node1.PNG)

Receipt of wei in Metamask account for node 2:

![Metamask Account- ETH mined Node 2](https://github.com/Renumelb/HW18/blob/main/Screenshots/Metamasknode2.PNG)

## Step 5: Metamask Account- Connect nodes  <a name="paragraph6"></a>


Please import the node keys into Metamask so that the mined ETH can be received into your account. To do this, please select the "Import" option and follow next steps.

![Metamask- Import Account- Node keys](https://github.com/Renumelb/HW18/blob/main/Screenshots/Metamaskimport1.PNG)


Then select json file from the dropdown and navigate to the folder where the nodes have been created. 

![Metamask- Import Account- Node keys](https://github.com/Renumelb/HW18/blob/main/Screenshots/Metamaskimport2.PNG)

Select the key stored in the "Keystore" folder and enter the node password as set up in Step 1

![Metamask- Import Account- Node keys](https://github.com/Renumelb/HW18/blob/main/Screenshots/metamaskimport3.PNG)

Please ensure that you have imported keys for both nodes.

## Step 6: Metamask Account- Add new genesis network finalnet  <a name="paragraph7"></a>

To set the Metamask network to the configured genesis, finalnet, please execute following steps:

Select add network:

![Metamask- Add network](https://github.com/Renumelb/HW18/blob/main/Screenshots/metamaskaddnetwork1.PNG)

Enter details of finalnet:

![Metamask- Add network](https://github.com/Renumelb/HW18/blob/main/Screenshots/Metamaskaddnetwork2.PNG)


## Step 7: Perform a Transaction in Metamask  <a name="paragraph8"></a>

We will now send 245678 wei from Node 1 to Node 2.

![Metamask- Perform transaction](https://github.com/Renumelb/HW18/blob/main/Screenshots/Send%20txn.PNG)

