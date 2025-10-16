// SPDX-License-Identifier
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
