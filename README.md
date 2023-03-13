Two coroutines are started to control the NPC's behavior. The first coroutine generates a random message from a list of messages and creates a chat bubble above the NPC's head with the message. The chat bubble is destroyed after 7 seconds. The second coroutine generates a random direction and moves the NPC towards a new position every 33 seconds.

Another coroutine is started to check if any NPCs have been destroyed. If an NPC's health is zero, it is destroyed.

Add Noob NPC to world from library
add this script to the workspace
click the plus button next to workspace and select script
paste below in and click run

```
local terrain = workspace.Terrain

local messages = {
	"Hello!",
	"How are you?",
	"I'm doing great!",
	"This is a nice day.",
	"I like your outfit.",
	"What brings you here?",
	"I'm so bored.",
	"I could really go for a burger.",
	"Do you like this game?",
	"I'm a little lost.",
	"What's your favorite color?",
	"I'm feeling lucky today.",
	"Have you seen any good movies lately?",
	"I'm looking for something fun to do.",
	"Have you tried the new update?",
	"This is my favorite game!",
	"I'm feeling a little down today.",
	"I need a vacation.",
	"What's your name?",
	"I hope you're having a great day!",
}

local noobs = {}

-- Function to create a chat bubble above an NPC's head
local function createChatBubble(npc, message)
	local chatBubble = Instance.new("BillboardGui")
	chatBubble.Size = UDim2.new(0, 175, 0, 80)
	chatBubble.StudsOffset = Vector3.new(0, 25, 0)
	chatBubble.Adornee = npc.PrimaryPart
	chatBubble.AlwaysOnTop = true
	chatBubble.Parent = npc

	local textLabel = Instance.new("TextLabel")
	textLabel.BackgroundTransparency = .2
	textLabel.Size = UDim2.new(1, 0, 1, 0)
	textLabel.TextColor3 = Color3.new(0, 0, 0)
	textLabel.BackgroundColor = BrickColor.new(1, 1, 1)

	textLabel.Font = Enum.Font.SourceSansBold
	textLabel.TextScaled = true
	textLabel.Text = message
	textLabel.Parent = chatBubble

	-- Destroy the chat bubble after a delay
	wait(7)
	chatBubble:Destroy()
end

while true do
	wait(.1)
	if math.random(7) == 2 then
		continue
	end
	local x = math.random(400)-math.random(400)
	local z = math.random(400)-math.random(400)

	local position = Vector3.new(x, 3, z)

	-- Create NPC
	local npc = workspace.Noob:Clone()
	npc.Name = "NPC"
	npc.Humanoid.Health = math.random(175)
	npc.Parent = workspace
	table.insert(noobs, npc)
	npc:SetPrimaryPartCFrame(CFrame.new(position))

	-- Create chat bubble
	local message = messages[math.random(#messages)]
	createChatBubble(npc, message)
end

