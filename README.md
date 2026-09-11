-- Скрипт для создания интерфейса Roblox в стиле Vega Scripts
-- Разместите этот LocalScript в StarterPlayer.StarterGui

local Players = game:GetService("Players")
local TweenService = game:GetService("TweenService")
local player = Players.LocalPlayer
local playerGui = player:WaitForChild("PlayerGui")

-- Настройки UI
local FONT = Enum.Font.Roboto
local TEXT_COLOR = Color3.fromRGB(255, 255, 255)
local BACKGROUND_COLOR = Color3.fromRGB(20, 20, 20)
local ACCENT_COLOR = Color3.fromRGB(100, 100, 100) -- Цвет при наведении
local HEADER_COLOR = Color3.fromRGB(30, 30, 30)

-- Функции для анимации
local function createTween(object, duration, properties)
	local tweenInfo = TweenInfo.new(duration, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
	return TweenService:Create(object, tweenInfo, properties)
end

-- === Создание основного GUI ===
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "ExploitMenuGui"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = playerGui

-- === Главный фрейм (Основное окно) ===
local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Size = UDim2.new(0, 450, 0, 300)
MainFrame.Position = UDim2.new(0.5, -225, 0.5, -150)
MainFrame.BackgroundColor3 = BACKGROUND_COLOR
MainFrame.BorderSizePixel = 0
MainFrame.ClipsDescendants = true
MainFrame.Active = true -- Чтобы можно было перетаскивать (если добавить скрипт драга)
MainFrame.Parent = ScreenGui

-- Добавляем эффект тени
local DropShadow = Instance.new("ImageLabel")
DropShadow.Name = "DropShadow"
DropShadow.AnchorPoint = Vector2.new(0.5, 0.5)
DropShadow.Position = UDim2.new(0.5, 0, 0.5, 5)
DropShadow.Size = UDim2.new(1, 20, 1, 20)
DropShadow.Image = "rbxassetid://1316045217" -- Стандартная тень Roblox
DropShadow.ImageColor3 = Color3.fromRGB(0, 0, 0)
DropShadow.ImageTransparency = 0.7
DropShadow.BackgroundTransparency = 1
DropShadow.ZIndex = MainFrame.ZIndex - 1
DropShadow.Parent = MainFrame

-- Заголовок
local Header = Instance.new("Frame")
Header.Name = "Header"
Header.Size = UDim2.new(1, 0, 0, 40)
Header.BackgroundColor3 = HEADER_COLOR
Header.BorderSizePixel = 0
Header.Parent = MainFrame

local Icon = Instance.new("ImageLabel")
Icon.Name = "Icon"
Icon.Size = UDim2.new(0, 24, 0, 24)
Icon.Position = UDim2.new(0, 10, 0.5, -12)
Icon.Image = "rbxassetid://13758779678" -- Иконка звезды, похожая на оригинал
Icon.BackgroundTransparency = 1
Icon.Parent = Header

local Title = Instance.new("TextLabel")
Title.Name = "Title"
Title.Size = UDim2.new(0, 200, 1, 0)
Title.Position = UDim2.new(0, 40, 0, 0)
Title.Text = "Vega Scripts"
Title.Font = FONT
Title.TextSize = 16
Title.TextColor3 = TEXT_COLOR
Title.TextXAlignment = Enum.TextXAlignment.Left
Title.BackgroundTransparency = 1
Title.Parent = Header

-- Кнопки окна (свернуть, развернуть, закрыть)
local WindowButtons = Instance.new("Frame")
WindowButtons.Name = "WindowButtons"
WindowButtons.Size = UDim2.new(0, 80, 1, 0)
WindowButtons.Position = UDim2.new(1, -80, 0, 0)
WindowButtons.BackgroundTransparency = 1
WindowButtons.Parent = Header

local function createWindowBtn(name, char, xPos)
	local btn = Instance.new("TextButton")
	btn.Name = name
	btn.Text = char
	btn.Font = Enum.Font.Code
	btn.TextSize = 18
	btn.TextColor3 = TEXT_COLOR
	btn.Size = UDim2.new(0, 25, 1, 0)
	btn.Position = UDim2.new(0, xPos, 0, 0)
	btn.BackgroundTransparency = 1
	
	-- Анимация наведения
	btn.MouseEnter:Connect(function()
		createTween(btn, 0.1, {TextColor3 = ACCENT_COLOR}):Play()
	end)
	btn.MouseLeave:Connect(function()
		createTween(btn, 0.1, {TextColor3 = TEXT_COLOR}):Play()
	end)
	-- Функционал закрытия (просто скрываем GUI)
	if name == "CloseBtn" then
		btn.MouseButton1Click:Connect(function()
			ScreenGui.Enabled = false
		end)
	end
	
	btn.Parent = WindowButtons
end
createWindowBtn("MinimizeBtn", "—", 5)
createWindowBtn("MaximizeBtn", "🗖", 30)
createWindowBtn("CloseBtn", "✕", 55)

-- Подзаголовок (Discord)
local DiscordSub = Instance.new("TextLabel")
DiscordSub.Name = "DiscordSub"
DiscordSub.Size = UDim2.new(1, 0, 0, 15)
DiscordSub.Position = UDim2.new(0, 10, 0, 45)
DiscordSub.Text = "discord.gg/vega-scripts"
DiscordSub.Font = FONT
DiscordSub.TextSize = 12
DiscordSub.TextColor3 = Color3.fromRGB(150, 150, 150)
DiscordSub.TextXAlignment = Enum.TextXAlignment.Left
DiscordSub.BackgroundTransparency = 1
DiscordSub.Parent = MainFrame

-- === Левая навигация ===
local LeftNav = Instance.new("Frame")
LeftNav.Name = "LeftNav"
LeftNav.Size = UDim2.new(0, 130, 1, -65) -- Отступ для хедера
LeftNav.Position = UDim2.new(0, 0, 0, 65)
LeftNav.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
LeftNav.BorderSizePixel = 0
LeftNav.Parent = MainFrame

local NavButton = Instance.new("TextButton")
NavButton.Name = "NavButton"
NavButton.Size = UDim2.new(1, 0, 0, 35)
NavButton.Position = UDim2.new(0, 0, 0, 10)
NavButton.Text = "   Trade Scam" -- Пробелы для отступа
NavButton.Font = FONT
NavButton.TextSize = 14
NavButton.TextColor3 = TEXT_COLOR
NavButton.TextXAlignment = Enum.TextXAlignment.Left
NavButton.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
NavButton.BorderSizePixel = 0
NavButton.Parent = LeftNav

local NavIcon = Instance.new("ImageLabel")
NavIcon.Name = "Icon"
NavIcon.Size = UDim2.new(0, 16, 0, 16)
NavIcon.Position = UDim2.new(0, 10, 0.5, -8)
NavIcon.Image = "rbxassetid://3926305904" -- Иконка щита/замка (пример)
NavIcon.ImageRectOffset = Vector2.new(644, 684) -- Выбор иконки из спрайта
NavIcon.ImageRectSize = Vector2.new(36, 36)
NavIcon.BackgroundTransparency = 1
NavIcon.Parent = NavButton

-- === Правая область контента ===
local ContentArea = Instance.new("Frame")
ContentArea.Name = "ContentArea"
ContentArea.Size = UDim2.new(1, -140, 1, -75) -- Отступы для навигации
ContentArea.Position = UDim2.new(0, 135, 0, 75)
ContentArea.BackgroundTransparency = 1
ContentArea.Parent = MainFrame

-- === Раздел Trade Scam Features (Выпадающий список) ===
local FeaturesContainer = Instance.new("Frame")
FeaturesContainer.Name = "FeaturesContainer"
FeaturesContainer.Size = UDim2.new(1, 0, 0, 30)
FeaturesContainer.BackgroundTransparency = 1
FeaturesContainer.Parent = ContentArea

local DropdownHeader = Instance.new("TextButton")
DropdownHeader.Name = "DropdownHeader"
DropdownHeader.Size = UDim2.new(1, 0, 1, 0)
DropdownHeader.Text = "   Trade Scam Features" -- Пробел для отступа
DropdownHeader.Font = FONT
DropdownHeader.TextSize = 14
DropdownHeader.TextColor3 = TEXT_COLOR
DropdownHeader.TextXAlignment = Enum.TextXAlignment.Left
DropdownHeader.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
DropdownHeader.BorderSizePixel = 0
DropdownHeader.Parent = FeaturesContainer

local Arrow = Instance.new("TextLabel")
Arrow.Name = "Arrow"
Arrow.Text = ">"
Arrow.Font = Enum.Font.Code
Arrow.TextSize = 16
Arrow.TextColor3 = TEXT_COLOR
Arrow.Size = UDim2.new(0, 20, 1, 0)
Arrow.Position = UDim2.new(1, -25, 0, 0)
Arrow.BackgroundTransparency = 1
Arrow.Parent = DropdownHeader

-- Секция контента внутри выпадающего списка
local FeaturesContent = Instance.new("Frame")
FeaturesContent.Name = "FeaturesContent"
FeaturesContent.Size = UDim2.new(1, 0, 0, 40) -- Изначальная высота контента
FeaturesContent.Position = UDim2.new(0, 0, 1, 0) -- Сразу под хедером
FeaturesContent.BackgroundColor3 = Color3.fromRGB(28, 28, 28) -- Немного темнее фона
FeaturesContent.BorderSizePixel = 0
FeaturesContent.Visible = false -- Изначально скрыто
FeaturesContent.Parent = FeaturesContainer

local DropdownUIPadding = Instance.new("UIPadding")
DropdownUIPadding.PaddingLeft = UDim.new(0, 10)
DropdownUIPadding.Parent = FeaturesContent

-- === Кнопка "Freeze Trade" ===
local FreezeBtn = Instance.new("TextButton")
FreezeBtn.Name = "FreezeTradeBtn"
FreezeBtn.Text = "Freeze Trade (Визуальная)"
FreezeBtn.Font = FONT
FreezeBtn.TextSize = 14
FreezeBtn.TextColor3 = TEXT_COLOR
FreezeBtn.Size = UDim2.new(1, -20, 0, 30)
FreezeBtn.Position = UDim2.new(0, 0, 0, 5) -- Отступ сверху
FreezeBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
FreezeBtn.BorderColor3 = Color3.fromRGB(60, 60, 60)
FreezeBtn.Parent = FeaturesContent

-- Логика выпадающего списка
local isExpanded = false
DropdownHeader.MouseButton1Click:Connect(function()
	isExpanded = not isExpanded
	
	if isExpanded then
		createTween(FeaturesContainer, 0.2, {Size = UDim2.new(1, 0, 0, 30 + FeaturesContent.Size.Y.Offset)}):Play()
		createTween(Arrow, 0.2, {Rotation = 90}):Play()
		FeaturesContent.Visible = true
	else
		createTween(FeaturesContainer, 0.2, {Size = UDim2.new(1, 0, 0, 30)}):Play()
		createTween(Arrow, 0.2, {Rotation = 0}):Play()
		FeaturesContent.Visible = false
	end
end)

-- === Раздел Information ===
local InfoContainer = Instance.new("Frame")
InfoContainer.Name = "InfoContainer"
InfoContainer.Size = UDim2.new(1, 0, 0, 30)
InfoContainer.Position = UDim2.new(0, 0, 0, 40) -- Ниже первого раздела
InfoContainer.BackgroundTransparency = 1
InfoContainer.Parent = ContentArea

local InfoHeader = Instance.new("TextButton")
InfoHeader.Name = "InfoHeader"
InfoHeader.Size = UDim2.new(1, 0, 1, 0)
InfoHeader.Text = "   Information"
InfoHeader.Font = FONT
InfoHeader.TextSize = 14
InfoHeader.TextColor3 = TEXT_COLOR
InfoHeader.TextXAlignment = Enum.TextXAlignment.Left
InfoHeader.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
InfoHeader.BorderSizePixel = 0
InfoHeader.Parent = InfoContainer

local InfoArrow = Instance.new("TextLabel")
InfoArrow.Name = "Arrow"
InfoArrow.Text = ">"
InfoArrow.Font = Enum.Font.Code
InfoArrow.TextSize = 16
InfoArrow.TextColor3 = TEXT_COLOR
InfoArrow.Size = UDim2.new(0, 20, 1, 0)
InfoArrow.Position = UDim2.new(1, -25, 0, 0)
InfoArrow.BackgroundTransparency = 1
InfoArrow.Parent = InfoHeader

-- === Добавление функционала перетаскивания (Draggable) ===
local dragging
local dragInput
local dragStart
local startPos

local function update(input)
	local delta = input.Position - dragStart
	MainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
end

Header.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
		dragging = true
		dragStart = input.Position
		startPos = MainFrame.Position
		input.Changed:Connect(function()
			if input.UserInputState == Enum.UserInputState.End then
				dragging = false
			end
		end)
	end
end)

Header.InputChanged:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
		dragInput = input
	end
end)

game:GetService("UserInputService").InputChanged:Connect(function(input)
	if input == dragInput and dragging then
		update(input)
	end
end)
