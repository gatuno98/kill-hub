-- Defina a classe ou objeto de um jogador
Player = {}
Player.__index = Player

-- Função para criar um novo jogador
function Player.new(name, x, y)
    local self = setmetatable({}, Player)
    self.name = name
    self.x = x
    self.y = y
    self.isAlive = true
    return self
end

-- Função para calcular a distância entre dois jogadores
function Player:distanceTo(otherPlayer)
    return math.sqrt((self.x - otherPlayer.x)^2 + (self.y - otherPlayer.y)^2)
end

-- Função para verificar a proximidade e "matar" o outro jogador
function Player:checkProximity(otherPlayer, killDistance)
    if self:distanceTo(otherPlayer) <= killDistance then
        otherPlayer:kill()
    end
end

-- Função que simula a morte de um jogador
function Player:kill()
    if self.isAlive then
        self.isAlive = false
        print(self.name .. " foi eliminado!")
    end
end

-- Exemplo de uso do script:

-- Criando dois jogadores
player1 = Player.new("Jogador 1", 0, 0)
player2 = Player.new("Jogador 2", 3, 4)  -- A distância entre (0,0) e (3,4) é 5 unidades

-- Definindo a distância de eliminação
killDistance = 5

-- Verificando se a proximidade é suficiente para "matar" o jogador
player1:checkProximity(player2, killDistance)

-- Resultado esperado: "Jogador 2 foi eliminado!" (pois a distância entre os jogadores é 5)
