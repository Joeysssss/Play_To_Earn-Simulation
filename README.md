# Play_To_Earn-Simulation
**References:** [How to Build a Play to Earn Blockchain Game]([https://ithelp.ithome.com.tw/articles/10297084](https://www.youtube.com/watch?v=iTfQh5m8HF8&t=2s)) <br>
## Mining Contract
1. Import thirdweb contract <br>
  ```
  import "@thirdweb-dev/contracts/drop/DropERC1155.sol"; // For my collection of Pickaxes <br>
  import "@thirdweb-dev/contracts/token/TokenERC20.sol"; // For my ERC-20 Token contract <br>
  import "@thirdweb-dev/contracts/openzeppelin-presets/utils/ERC1155/ERC1155Holder.sol";
  ```
2. Calculate Rewards <br>
  ```
      function calculateRewards(address _player) <br>
        public <br>
        view <br>
        returns (uint256 _rewards) <br>
    { <br>
        // If playerLastUpdate or playerPickaxe is not set, then the player has no rewards. <br>
        if ( <br>
            !playerLastUpdate[_player].isData || !playerPickaxe[_player].isData <br>
        ) { <br>
            return 0; <br>
        } <br>

        // Calculate the time difference between now and the last time they staked/withdrew/claimed their rewards <br>
        uint256 timeDifference = block.timestamp - <br>
            playerLastUpdate[_player].value;  <br>

        // Calculate the rewards they are owed <br>
        uint256 rewards = timeDifference * <br>
            10_000_000_000_000 * <br>
            (playerPickaxe[_player].value + 1); <br>

        // Return the rewards <br>
        return rewards; <br>
    } <br>
  ```
