// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

/// @title Supply Chain Tracker using Blockchain
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

    /// @notice Adds a new product to the supply chain
    function addProduct(string memory name, string memory location) public {
        productCount++;
        products[productCount] = Product(productCount, name, location, "Created", msg.sender);
        emit ProductAdded(productCount, name, msg.sender);
    }

    /// @notice Updates product status/location and transfers ownership
    function updateProduct(uint id, string memory newLocation, string memory newStatus, address newOwner) public {
        require(id > 0 && id <= productCount, "Invalid product ID");
        Product storage product = products[id];
        require(msg.sender == product.owner, "Only current owner can update");

        product.location = newLocation;
        product.status = newStatus;
        product.owner = newOwner;

        emit ProductUpdated(id, newLocation, newStatus, newOwner);
    }

    /// @notice Retrieves a product by ID
    function getProduct(uint id) public view returns (Product memory) {
        require(id > 0 && id <= productCount, "Invalid product ID");
        return products[id];
    }
}
