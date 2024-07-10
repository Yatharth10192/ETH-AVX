# MEDICAL RECORD 
This Solidity project is a smart contract named MedicalRecords which is designed to store and manage medical records on the Ethereum blockchain. 

# Description
A counter is made to keep track of the unique ID for each medical record namely recordId. We have the function that retrieves the name of the patient in a specific medical record.

# STEPS


npx hardhat help : This command provides help and displays the list of available commands and options in Hardhat, a development environment for compiling, deploying, testing, and debugging Ethereum software.
npx hardhat test : This command runs the tests defined for the Hardhat project. It's used to ensure that your smart contracts are functioning correctly by executing the test cases written in your project.
REPORT_GAS=true npx hardhat test : This command runs the tests while also reporting the gas usage for each operation. The REPORT_GAS=true environment variable enables gas reporting, which is useful for optimizing and understanding the cost of your smart contract functions.
npx hardhat node : This command starts a local Ethereum network node. 
npx hardhat run scripts/deploy.js : This command executes a script to deploy your smart contracts. The scripts/deploy.js file typically contains the deployment logic for your contracts, specifying which contracts to deploy and to which network (local or remote).

# Installing
We will require Node.js, npm and Hardhat. You can download and install Node.js from nodejs.org and npm is included with node.js
Hardhat is a development environment for Ethereum software. 

# Executing program
//SPDX-License-Identifier:MIT
pragma solidity ^0.8.0;

contract MedicalRecords {
    uint public recordId;
    mapping(uint => Record) records;
    mapping(uint => bool) public isDeleted;
    struct Record {
        uint recordId;
        uint timestamp;
        string name;
        uint age;
        string gender;
        string bloodType;
        string allergies;
        string diagnosis;
        string treatment;
    }

    event MedicalRecords__AddRecord(
        uint recordId,
        uint timestamp,
        string name,
        uint age,
        string gender,
        string bloodType,
        string allergies,
        string diagnosis,
        string treatment
    );
    event MedicalRecords__DeleteRecord(
        uint recordId,
        uint timestamp,
        string name,
        uint age,
        string gender,
        string bloodType,
        string allergies,
        string diagnosis,
        string treatment
    );

    function addRecord(
        string memory _name,
        uint _age,
        string memory _gender,
        string memory _bloodType,
        string memory _allergies,
        string memory _diagnosis,
        string memory _treatment
    ) public {
        recordId++;
        records[recordId] = Record(
            recordId,
            block.timestamp,
            _name,
            _age,
            _gender,
            _bloodType,
            _allergies,
            _diagnosis,
            _treatment
        );
        emit MedicalRecords__AddRecord(
            recordId,
            block.timestamp,
            _name,
            _age,
            _gender,
            _bloodType,
            _allergies,
            _diagnosis,
            _treatment
        );
    }

    function deleteRecord(uint _recordId) public {
        require(!isDeleted[_recordId], "The record is already deleted");
        Record storage record = records[_recordId];
        emit MedicalRecords__DeleteRecord(
            record.recordId,
            block.timestamp,
            record.name,
            record.age,
            record.gender,
            record.bloodType,
            record.allergies,
            record.diagnosis,
            record.treatment
        );
        isDeleted[_recordId] = true;
    }

    function getRecord(
        uint _recordId
    )
        public
        view
        returns (
            uint,
            string memory,
            uint,
            string memory,
            string memory,
            string memory,
            string memory,
            string memory
        )
    {
        Record storage record = records[_recordId];
        return (
            record.timestamp,
            record.name,
            record.age,
            record.gender,
            record.bloodType,
            record.allergies,
            record.diagnosis,
            record.treatment
        );
    }

    function getRecordId() public view returns (uint) {
        return recordId;
    }

    function getTimeStamp(uint _recordId) public view returns (uint) {
        return records[_recordId].timestamp;
    }

    function getName(uint _recordId) public view returns (string memory) {
        return records[_recordId].name;
    }

    function getAge(uint _recordId) public view returns (uint) {
        return records[_recordId].age;
    }

    function getGender(uint _recordId) public view returns (string memory) {
        return records[_recordId].gender;
    }

    function getBloodType(uint _recordId) public view returns (string memory) {
        return records[_recordId].bloodType;
    }

    function getAllergies(uint _recordId) public view returns (string memory) {
        return records[_recordId].allergies;
    }

    function getDiagnosis(uint _recordId) public view returns (string memory) {
        return records[_recordId].diagnosis;
    }

    function getTreatment(uint _recordId) public view returns (string memory) {
        return records[_recordId].treatment;
    }

    function getDeleted(uint256 _recordId) public view returns (bool) {
        return isDeleted[_recordId];
    }
}


## Authors
Yatharth Sharma
yatharths10192@gmail.com

## License

This project is licensed under the MIT License - see the LICENSE.md file for details
