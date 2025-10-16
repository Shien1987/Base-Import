# Base-Import
Base Import


// SPDX-License-Identifier: MIT
pragma solidity ^0.8.30;

/// @title SillyStringUtils2
/// @notice A library for silly string manipulations, including Haiku struct and shrug emoji appending.
library SillyStringUtils2 {
    /// @notice Struct representing a Haiku poem with three lines
    struct Haiku {
        string line1;
        string line2;
        string line3;
    }

    /// @notice Appends a shrugging emoji () to the input string
    /// @dev Uses unicode literal for the emoji, with a space before it for proper formatting
    /// @param _input The original string
    /// @return The string with space and shrug appended
    function shruggie(string memory _input) internal pure returns (string memory) {
        return string.concat(_input, " ", unicode"");
    }
}



// SPDX-License-Identifier: MIT
pragma solidity ^0.8.30;

// Importing the SillyStringUtils2 library
import "./SillyStringUtils2.sol";

/// @title ImportsExercise
/// @notice A simple contract for storing and manipulating Haikus using the SillyStringUtils2 library.
/// @dev Demonstrates library usage, struct handling, and string manipulation in Solidity.
contract ImportsExercise {
    /// @notice Using the SillyStringUtils2 library for string manipulation
    using SillyStringUtils2 for string;

    /// @notice Public variable to store a Haiku
    SillyStringUtils2.Haiku public haiku;

    /// @notice Emitted when a new Haiku is saved
    /// @param line1 The first line of the Haiku
    /// @param line2 The second line of the Haiku
    /// @param line3 The third line of the Haiku
    event HaikuSaved(string line1, string line2, string line3);

    /// @notice Saves a Haiku with three lines
    /// @dev Ensures lines are non-empty to avoid invalid states
    /// @param _line1 The first line (5 syllables ideally)
    /// @param _line2 The second line (7 syllables ideally)
    /// @param _line3 The third line (5 syllables ideally)
    function saveHaiku(
        string memory _line1,
        string memory _line2,
        string memory _line3
    ) public {
        require(bytes(_line1).length > 0, "Line 1 cannot be empty");
        require(bytes(_line2).length > 0, "Line 2 cannot be empty");
        require(bytes(_line3).length > 0, "Line 3 cannot be empty");

        haiku.line1 = _line1;
        haiku.line2 = _line2;
        haiku.line3 = _line3;

        emit HaikuSaved(_line1, _line2, _line3);
    }

    /// @notice Retrieves the saved Haiku
    /// @return The current Haiku struct
    function getHaiku() public view returns (SillyStringUtils2.Haiku memory) {
        return haiku;
    }

    /// @notice Appends a shrugging emoji to the third line of the Haiku
    /// @dev Creates a copy to avoid modifying the stored state
    /// @return A modified Haiku with shrug on line 3
    function shruggieHaiku() public view returns (SillyStringUtils2.Haiku memory) {
        SillyStringUtils2.Haiku memory newHaiku = haiku;
        newHaiku.line3 = newHaiku.line3.shruggie();
        return newHaiku;
    }
}
