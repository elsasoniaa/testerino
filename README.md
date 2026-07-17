### Recursos iniciales

- [Docs oficiales de Base](https://docs.base.org)
- [Build on Base](https://base.org/build)
- [Base Bridge](https://bridge.base.org)
- [Blockscout (explorador)](https://base.blockscout.com)

### Primera reflexión

Estoy empezando a entender mejor cómo funciona el ecosistema de Base. Este repo me sirve como cuaderno organizado para ir guardando todo lo que vaya aprendiendo paso a paso.

### Idea inicial de proyecto pequeño

Un "Hello Base" on-chain: 
- Contrato que guarda un mensaje
- Frontend simple para leer y actualizar el mensaje
- Desplegarlo en Base como primer experimento

### Stablecoins más usadas en Base

- USDC (nativo y muy líquido)
- USDT
- DAI

Son ideales para trading, pagos o evitar volatilidad mientras se aprende.

### Primera aproximación a Solidity

Solidity es el lenguaje principal para escribir contratos inteligentes en Base.

Características básicas:
- Similar a JavaScript en sintaxis
- Es fuertemente tipado
- Se compila a bytecode para la EVM

### Importancia de los eventos en contratos

Los eventos permiten que el frontend sepa cuándo pasa algo en el contrato (ej: un mint, un swap, un cambio de estado).

Son baratos y esenciales para construir dApps reactivas.

### Herramientas de desarrollo útiles

- Remix IDE → Para pruebas rápidas
- Hardhat → Para proyectos serios
- Foundry → Muy rápido para testing
- Ethers.js / Viem → Para frontend

- ### Importancia de verificar contratos

Verificar el código en Blockscout permite que cualquiera pueda leerlo y auditarlo.

Beneficios:
- Transparencia
- Mayor confianza de los usuarios
- Buena práctica profesional

### Introducción a los NFTs (ERC-721)

Los NFTs son tokens no fungibles. Cada uno es único.

En Base es muy barato mintear y transferir NFTs gracias a los bajos fees.

### Qué es un Liquidity Pool

Es un pool de fondos que permite hacer swaps en DEXs.

Al proporcionar liquidez recibes fees de las transacciones, pero también tienes riesgo de impermanent loss.

### Custodial vs Non-custodial wallets

- Custodial: La plataforma guarda tus claves (ej. algunos exchanges)
- Non-custodial: Tú controlas tus claves (MetaMask, Coinbase Wallet, etc.)

En crypto se recomienda siempre non-custodial.

### Idea de proyecto NFT simple

Crear una colección de "Builder Badges":
- Cada badge representa un nivel de aprendizaje
- Se mintean al completar hitos
- Todo on-chain en Base

- ### Contrato Counter simple (primer experimento)

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Counter {
    uint256 public count = 0;

    function increment() public {
        count += 1;
    }

    function decrement() public {
        count -= 1;
    }

    function reset() public {
        count = 0;
    }
}

**Mensaje:** `docs: script de despliegue básico con Hardhat`

**Texto para añadir:**

```markdown
### Script de despliegue básico (Hardhat)

```javascript
// deploy.js
const hre = require("hardhat");

async function main() {
  const Counter = await hre.ethers.getContractFactory("Counter");
  const counter = await Counter.deploy();

  await counter.deployed();
  console.log("Counter desplegado en:", counter.address);
}

main().catch((error) => {
  console.error(error);
  process.exit(1);
});

**Mensaje:** `docs: frontend básico para interactuar con Counter`

**Texto para añadir:**

```markdown
### Frontend básico para interactuar con el Counter

```html
<button onclick="increment()">Incrementar</button>
<p>Contador: <span id="value">0</span></p>

<script>
  // Código con ethers.js para llamar al contrato en Base
</script>

```markdown
### Idea de mejora al Counter

Añadir:
- Eventos cuando se modifica el contador
- Ownership (solo owner puede resetear)
- Contador por usuario

Esto lo haría más útil como proyecto de práctica.

### Frontend básico para SimpleStorage

```html
<input id="input" placeholder="Nuevo mensaje" />
<button onclick="setData()">Guardar</button>
<p id="display"></p>

<script>
  // Conectar wallet y llamar setData / getData
</script>
### Ejemplo de conexión con ethers.js

```javascript
const provider = new ethers.providers.Web3Provider(window.ethereum);
const signer = provider.getSigner();

const contract = new ethers.Contract(address, abi, signer);

await contract.register(); // Llamada al contrato

### Script para verificar contrato en Blockscout

Usando Hardhat:

```bash
npx hardhat verify --network base <contract_address> <constructor_args>

### Frontend con botón de stake

```html
<button onclick="stakeTokens()">Stake Tokens</button>

<script>
async function stakeTokens() {
  const amount = document.getElementById("amount").value;
  await contract.stake(ethers.utils.parseEther(amount));
}
</script>
### Script para deploy en diferentes redes

```javascript
// hardhat.config.js ejemplo
networks: {
  base: {
    url: "https://mainnet.base.org",
    accounts: [privateKey]
  },
  baseSepolia: { // testnet
    url: "https://sepolia.base.org",
    accounts: [privateKey]
  }
}
### Frontend mostrando balance

```html
<p>Tu balance: <span id="balance">0</span> ETH</p>

<script>
async function updateBalance() {
  const balance = await provider.getBalance(address);
  document.getElementById("balance").innerText = ethers.utils.formatEther(balance);
}
</script>

### Frontend con estado de loading

```html
<button onclick="sendTx()" id="btn">Enviar</button>

<script>
async function sendTx() {
  document.getElementById("btn").disabled = true;
  document.getElementById("btn").innerText = "Procesando...";
  // await transaction
  document.getElementById("btn").disabled = false;
  document.getElementById("btn").innerText = "Enviar";
}
</script>

### Botón de conexión de wallet mejorado

```html
<button onclick="connectWallet()">Connect Wallet</button>

<script>
async function connectWallet() {
  if (window.ethereum) {
    await window.ethereum.request({ method: 'eth_requestAccounts' });
    // actualizar UI
  }
}
</script>

### Mostrar estado de transacción en frontend

```javascript
const tx = await contract.increment();
await tx.wait(); // espera confirmación
console.log("Transacción confirmada en Base");

### Error handling en frontend

```javascript
try {
  const tx = await contract.functionCall();
  await tx.wait();
} catch (error) {
  console.error("Error en Base:", error.message);
  alert("Transacción fallida. Revisa el gas o permisos.");
}

### Frontend mostrando lista on-chain

```javascript
async function loadNumbers() {
  const count = await contract.getCount();
  for(let i = 0; i < count; i++) {
    const num = await contract.numbers(i);
    // mostrar en UI
  }
}

### Múltiples llamadas a contratos

```javascript
const [balance, count, status] = await Promise.all([
  contract.balanceOf(address),
  counter.count(),
  anotherContract.status()
]);

### Llamando múltiples contratos desde frontend

```javascript
const usdcBalance = await usdcContract.balanceOf(address);
const counterValue = await counterContract.count();

### Withdraw Pattern (seguridad)

```solidity
mapping(address => uint256) public balances;

function withdraw() public {
    uint256 amount = balances[msg.sender];
    balances[msg.sender] = 0; // reentrancy protection
    payable(msg.sender).transfer(amount);
}

### Llamadas en batch desde frontend

```javascript
const calls = [
  contract.populateTransaction.increment(),
  contract.populateTransaction.increment()
];

const tx = await signer.sendTransaction({
  to: contract.address,
  data: // encoded batch
});

### Frontend para entrar en raffle

```html
<button onclick="enterRaffle()">Participar (0.01 ETH)</button>

<script>
async function enterRaffle() {
  await contract.enter({ value: ethers.utils.parseEther("0.01") });
}
</script>

### Frontend con sistema de referral

```html
<p>Tu link de referral: <span id="link">https://.../ref=0x...</span></p>
<button onclick="copyLink()">Copiar</button>
### Mostrar cooldown en frontend

```javascript
const timeLeft = lastAction + cooldown - Date.now()/1000;
document.getElementById("cooldown").innerText = timeLeft > 0 ? `${timeLeft}s` : "Ready";

### Solicitud de firma desde frontend

```javascript
const signature = await signer.signMessage("Firma esta acción...");

### Frontend para solicitar random

```javascript
async function getRandomNumber() {
  const tx = await contract.requestRandomWords();
  await tx.wait();
  // esperar callback del oráculo
}

### Frontend mostrando precio en tiempo real

```javascript
async function updatePrice() {
  const price = await contract.getPrice();
  document.getElementById("price").innerText = price / 1e8; // ajustar decimals
}

### Slippage tolerance en frontend

```html
<label>Slippage %: <input type="number" value="0.5" id="slippage" /></label>

<script>
const maxSlippage = document.getElementById("slippage").value;
</script>

### Mostrar tax en frontend

```html
<p>Tax on transfer: 5%</p>
<p>Amount received: <span id="received"></span></p>

<script>
function calculateReceived(amount) {
  const tax = amount * 0.05;
  document.getElementById("received").innerText = amount - tax;
}
</script>
