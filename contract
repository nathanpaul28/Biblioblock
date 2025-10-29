// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

/// @title Biblioblock - Immutable Book Lending Registry
/// @author 
/// @notice This contract records book lending and returning events on-chain.
/// @dev Basic version suitable for Solidity beginners.

contract Biblioblock {

    // --- STRUCTS ---
    struct Book {
        uint id;
        string title;
        string author;
        string isbn;
        bool exists;
    }

    struct LendingRecord {
        uint bookId;
        address borrower;
        uint timestamp;
        string status; // "LENT" or "RETURNED"
    }

    // --- STATE VARIABLES ---
    uint public bookCount;
    mapping(uint => Book) public books;
    LendingRecord[] public lendingHistory;

    // --- EVENTS ---
    event BookAdded(uint bookId, string title, string author);
    event BookLent(uint bookId, address borrower, uint timestamp);
    event BookReturned(uint bookId, address borrower, uint timestamp);

    // --- FUNCTIONS ---

    /// @notice Add a new book to the registry
    function addBook(string memory _title, string memory _author, string memory _isbn) public {
        bookCount++;
        books[bookCount] = Book(bookCount, _title, _author, _isbn, true);
        emit BookAdded(bookCount, _title, _author);
    }

    /// @notice Lend a book to someone
    function lendBook(uint _bookId) public {
        require(books[_bookId].exists, "Book does not exist");
        lendingHistory.push(LendingRecord(_bookId, msg.sender, block.timestamp, "LENT"));
        emit BookLent(_bookId, msg.sender, block.timestamp);
    }

    /// @notice Return a book
    function returnBook(uint _bookId) public {
        require(books[_bookId].exists, "Book does not exist");
        lendingHistory.push(LendingRecord(_bookId, msg.sender, block.timestamp, "RETURNED"));
        emit BookReturned(_bookId, msg.sender, block.timestamp);
    }

    /// @notice Get total lending records
    function getLendingCount() public view returns (uint) {
        return lendingHistory.length;
    }

    /// @notice Get lending record by index
    function getLendingRecord(uint index) public view returns (LendingRecord memory) {
        require(index < lendingHistory.length, "Invalid index");
        return lendingHistory[index];
    }
}
