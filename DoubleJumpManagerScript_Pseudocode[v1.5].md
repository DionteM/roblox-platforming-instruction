### DoubleJumpManagerScript - Pesudocode

1.  Create a `local` variable named `ReplicatedStorage` and set it to the following. `game` is a global instance it has a function inside of it called `:GetService()` use this function on the instance with `"ReplicatedStorage"` as an input

2. Create a `local` variable named `PlayerService` and set it to the following. `game` is a global instance it has a function inside of it called `:GetService()` use this function on the instance with `"Players"` as an input

3.  Create a `local` variable named `MarketplaceService` and set it to the following. `game` is a global instance it has a function inside of it called `:GetService()` use this function on the instance with `"MarketplaceService"` as an input

4.  Create a `local` variable named `settings` and set it to the following. `require()` is a global function the following code should be put as an input. `ReplicatedStorage` is an instance it has a function inside of it called `:WaitForChild()` use this function on the instance with `"DoubleJumpSettings",30` as an input

5.  Create a `local` variable named `event` and set it to the following. `ReplicatedStorage` is an instance it has a function inside of it called `:WaitForChild()` use this function on the instance with `"DoubleJumpEvent",60` as an input

6. Connect to an event called `.PlayerAdded`  that's inside of `PlayerService` with  `player` as an input. There's a **hint** below
```lua
PlayerSerivce.PlayerAdded:Connect(function(players)
end)
```
7.) Create a `local` varaible named `canUse` and set it to `true`

8.) Create a conditional `if` statement. Inside it should check the following. `#settings.WhiteList > 0` you should `then`

9.) `canUse` is a variable you need to set it to `false`

10.) Lines **10-15** are freebies below.

```lua
for _,id in pairs(settings.WhiteList) do
			if id == player.UserId then
				canUse = true
				break
			end
		end
```
16. You can `end` the conditional statement from line **8.** here
17.) Create a conditional `if` statement. Inside it should check the following. `true` you should `then`
18.)  Lines **18-23** are shown below to copy and paste.

```lua
player.CharacterAdded:Connect(function(char)
			script["DoubleJump"]:Clone().Parent = char
		end)
		if player.Character then
			script["DoubleJump"]:Clone().Parent = player.Character
		end
```
