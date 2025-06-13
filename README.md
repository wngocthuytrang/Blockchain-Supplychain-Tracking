# Blockchain in Supply Chain Transparency

## Introduction

In the era of globalization, supply chains play a pivotal role in the transportation of goods between countries and regions. However, traditional supply chain systems are facing many problems such as counterfeiting, lack of transparency, and lack of traceability. This is especially serious in industries such as healthcare, food, and fashion.

Blockchain – a distributed ledger technology, with immutable and transparent characteristics – has become a promising solution to solve the above problems. By recording every event in the product transportation process on the blockchain, stakeholders can verify the entire history of a product, from the place of production to the consumer.

## Contents

***1. Problems in traditional supply chains***

&emsp;• Counterfeit goods penetrate the market easily.
  
&emsp;• Manual, outdated inspection process.
  
&emsp;• Lack of clear ownership verification tools.
  
&emsp;• Data is fragmented among many intermediaries.

***2. Blockchain solution principles***

&emsp;• Each product is associated with a unique ID.

&emsp;• All activities (creation, movement, transfer, status change) are recorded as events.

&emsp;• Records are stored on the blockchain, public and immutable.

***3. Solution architecture***
![bfcdeaed-2123-43a6-abca-46a363ca8b8a](https://github.com/user-attachments/assets/6374ed2f-fb51-4348-bd08-c71a3b7176e2)
***4. Smart contract code (Solidity)***

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SupplyChain {
    struct Product {
        uint id;
        string name;
        string location;
        string status;
        address owner;
    }

    uint public productCount;
    mapping(uint => Product) public products;

    event ProductAdded(uint id, string name, address indexed owner);
    event ProductUpdated(uint id, string location, string status, address indexed newOwner);

    function addProduct(string memory name, string memory location) public {
        productCount++;
        products[productCount] = Product(productCount, name, location, "Created", msg.sender);
        emit ProductAdded(productCount, name, msg.sender);
    }

    function updateProduct(uint id, string memory newLocation, string memory newStatus, address newOwner) public {
        require(id > 0 && id <= productCount, "ID sản phẩm không hợp lệ");
        Product storage product = products[id];
        require(msg.sender == product.owner, "Chỉ chủ sở hữu hiện tại mới được cập nhật");

        product.location = newLocation;
        product.status = newStatus;
        product.owner = newOwner;

        emit ProductUpdated(id, newLocation, newStatus, newOwner);
    }

    function getProduct(uint id) public view returns (Product memory) {
        require(id > 0 && id <= productCount, "ID sản phẩm không hợp lệ");
        return products[id];
    }
}
```

***5. User Interface and Practical Applications***

&emsp;• Product Management Page (Portal)

&emsp;• Map displaying the journey (Map)

&emsp;• Product inspection tool using QR code

&emsp;• Easy integration with ERP, IoT sensors

***6. Technology and Tools***

&emsp;• Solidity, Ethereum, Web3.js/Ethers.js

&emsp;• React, IPFS, QR Code API

&emsp;• Truffle or Hardhat for contract compilation and deployment

***7. Other application areas***

&emsp;• Vaccine and medical drug tracking

&emsp;• Branded product authentication, high-end products

Electronic device management, warranty lifecycle

## Conclusion

Blockchain technology offers a breakthrough solution to the problem of supply chain transparency. Instead of relying on trust between parties, the system will be built on immutable records, allowing verification and auditing at any time.

The proposed solution is not only suitable for sensitive industries such as pharmaceuticals and food, but can also be expanded to any field that needs to control the origin of products. The application of smart contracts helps automate and save operating costs, while improving the consumer experience.

Personally, I believe that blockchain will soon become the new standard for supply chain management. Enterprises that are at the forefront of application will not only increase their reputation but also build a transparent, sustainable and competitive ecosystem in the digital age.
