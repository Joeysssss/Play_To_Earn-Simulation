# Play_To_Earn-Simulation
**References:** [How to Build a Play to Earn Blockchain Game]([https://ithelp.ithome.com.tw/articles/10297084](https://www.youtube.com/watch?v=iTfQh5m8HF8&t=2s)) <br>
## Mining Contract
1. Import thirdweb contract <br>
  ```
  import "@thirdweb-dev/contracts/drop/DropERC1155.sol"; // For my collection of Pickaxes 
  import "@thirdweb-dev/contracts/token/TokenERC20.sol"; // For my ERC-20 Token contract 
  import "@thirdweb-dev/contracts/openzeppelin-presets/utils/ERC1155/ERC1155Holder.sol";
  ```
2. Calculate Rewards <br>
  ```
      function calculateRewards(address _player) 
        public 
        view 
        returns (uint256 _rewards) 
    { 
        // If playerLastUpdate or playerPickaxe is not set, then return 0. 
        if ( 
            !playerLastUpdate[_player].isData || !playerPickaxe[_player].isData 
        ) { 
            return 0; 
        } 

        // Calculate the time difference between now and the last time they staked/withdrew/claimed their rewards 
        uint256 timeDifference = block.timestamp - 
            playerLastUpdate[_player].value;  

        // Calculate the rewards  
        uint256 rewards = timeDifference * 
            10_000_000_000_000 * 
            (playerPickaxe[_player].value + 1); 

        // Return the rewards 
        return rewards; 
    } <br>
  ```
## UI
1. open UI server 
```
  yarn dev
```
![UI](https://raw.githubusercontent.com/Joeysssss/Play_To_Earn-Simulation/main/photo/game.jpg "Equip")
![UI](https://raw.githubusercontent.com/Joeysssss/Play_To_Earn-Simulation/main/photo/Owned.jpg "Owned")
![UI](https://raw.githubusercontent.com/Joeysssss/Play_To_Earn-Simulation/main/photo/Shop.jpg "Shop")
