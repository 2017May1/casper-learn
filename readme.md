# Get Started With Casper (First 100 Submissions)


## 1. Create and deploy a simple, smart contract with cargo casper and cargo test




![](imgs/start.png)



### Create and deploy a simple, smart contract


![](imgs/deploy.png)

### Check Deploy Status

![](imgs/get-deploy.png)




## 2. Complete one of the existing tutorials for writing smart contracts
Key-Value Storage Tutorial

Building the Contract
![](imgs/kv-prepare.png)

Testing the Contract
![](imgs/kv-test.png)

Deploy the Contract
![](imgs/kv-deploy.png)



## 3. Demonstrate key management concepts by modifying the client in the Multi-Sig tutorial to address one of the additional scenarios

Scenario 5: 


```
const keyManager = require('./key-manager');
const TRANSFER_AMOUNT = process.env.TRANSFER_AMOUNT || 2500000000;

(async function () {
    
    // In this example the 2 additional accounts will be added to 
    // the mainAccount to perform deploys, but they will not be 
    // able to add another account. 
    
    // To achive the task, we will:
    // 1. Add first new key with weight 1 (first account).
    // 2. Add second new key with weight 3 (second account).
    // 3. Set mainAccount's weight to 1
    // 4. Add second new key with weight 3 (third account).
    // 5. Add second new key with weight 3 (fourth account)
    // 6. Set Keys Management Threshold to 3.
    // 7. Set Deploy Threshold to 2.


    let deploy;

    // 0. Initial state of the account.
    // There should be only one associated key (facuet) with weight 1.
    // Deployment Threshold should be set to 1.
    // Key Management Threshold should be set to 1.
    let masterKey = keyManager.randomMasterKey();
    let mainAccount = masterKey.deriveIndex(1);
    let firstAccount = masterKey.deriveIndex(2);
    let secondAccount = masterKey.deriveIndex(3);
    let thirdAccount = masterKey.deriveIndex(4);
    let fourthAccount = masterKey.deriveIndex(5)


    console.log("\n0.1 Fund main account.\n");
    await keyManager.fundAccount(mainAccount);
    await keyManager.printAccount(mainAccount);
    
    console.log("\n[x]0.2 Install Keys Manager contract");
    deploy = keyManager.keys.buildContractInstallDeploy(mainAccount);
    await keyManager.sendDeploy(deploy, [mainAccount]);
    await keyManager.printAccount(mainAccount);

    // 1. Add first new key with weight 1 (first account).
    console.log("\n1. Add first new key with weight 1.\n");
    deploy = keyManager.keys.setKeyWeightDeploy(mainAccount, firstAccount, 1);
    await keyManager.sendDeploy(deploy, [mainAccount]);
    await keyManager.printAccount(mainAccount);
    
    // 2. Add second new key with weight 3 (second account).
    console.log("\n2. Add second new key with weight 3.\n");
    deploy = keyManager.keys.setKeyWeightDeploy(mainAccount, secondAccount, 3);
    await keyManager.sendDeploy(deploy, [mainAccount]);
    await keyManager.printAccount(mainAccount);

    // 3. Set mainAccount's weight to 1
    console.log("\n3. Set faucet's weight to 1\n");
    deploy = keyManager.keys.setKeyWeightDeploy(mainAccount, mainAccount, 1);
    await keyManager.sendDeploy(deploy, [mainAccount]);
    await keyManager.printAccount(mainAccount);
    

    // 4. Add second new key with weight 3 (third account).
    console.log("\n4. Add second new key with weight 3.\n");
    deploy = keyManager.keys.setKeyWeightDeploy(mainAccount, thirdAccount, 3);
    await keyManager.sendDeploy(deploy, [mainAccount]);
    await keyManager.printAccount(mainAccount);

    // 5. Add second new key with weight 3 (fourth account).
    console.log("\n5. Add second new key with weight 3.\n");
    deploy = keyManager.keys.setKeyWeightDeploy(mainAccount, fourthAccount, 3);
    await keyManager.sendDeploy(deploy, [mainAccount]);
    await keyManager.printAccount(mainAccount);


    // 6. Set Keys Management Threshold to 3.
    console.log("\n6. Set Keys Management Threshold to 3\n");
    deploy = keyManager.keys.setKeyManagementThresholdDeploy(mainAccount, 3);
    await keyManager.sendDeploy(deploy, [mainAccount]);
    await keyManager.printAccount(mainAccount);
    
    // 7. Set Deploy Threshold to 2.
    console.log("\n7. Set Deploy Threshold to 2.\n");
    deploy = keyManager.keys.setDeploymentThresholdDeploy(mainAccount, 2);
    await keyManager.sendDeploy(deploy, [fourthAccount]);
    await keyManager.printAccount(mainAccount);

    

    
  
})();



```


![](imgs/scenario.png)

## 4. Learn to transfer tokens to an account on the Casper Testnet. Check out this documentation.


![](imgs/transfer.png)![](imgs/show-transfer.png)




## 5.Learn to Delegate and Undelegate on the Casper Testnet. Check out these instructions.



![](imgs/delegation.png)



![](imgs/undelegation.png)
