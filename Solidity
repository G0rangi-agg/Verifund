// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Verifund {
    struct Campaign {
        string name;
        string description;
        uint256 goal;
        uint256 raised;
        address payable owner;
    }
    
    Campaign[] public campaigns;
    
    event CampaignCreated(uint256 indexed campaignId, string name, address owner);
    event DonationReceived(uint256 indexed campaignId, address indexed donor, uint256 amount);
    
    function createCampaign(string memory _name, string memory _description, uint256 _goal) public {
        Campaign memory newCampaign = Campaign({
            name: _name,
            description: _description,
            goal: _goal,
            raised: 0,
            owner: payable(msg.sender)
        });
        
        campaigns.push(newCampaign);
        emit CampaignCreated(campaigns.length - 1, _name, msg.sender);
    }
    
    function donate(uint256 campaignId) public payable {
        require(campaignId < campaigns.length, "Campaign does not exist");
        require(msg.value > 0, "Donation must be greater than 0");
        
        campaigns[campaignId].raised += msg.value;
        campaigns[campaignId].owner.transfer(msg.value);
        
        emit DonationReceived(campaignId, msg.sender, msg.value);
    }
    
    function getCampaignCount() public view returns (uint256) {
        return campaigns.length;
    }
    
    function getCampaign(uint256 campaignId) public view returns (
        string memory name,
        string memory description,
        uint256 goal,
        uint256 raised,
        address owner
    ) {
        require(campaignId < campaigns.length, "Campaign does not exist");
        Campaign memory campaign = campaigns[campaignId];
        return (campaign.name, campaign.description, campaign.goal, campaign.raised, campaign.owner);
    }
}
