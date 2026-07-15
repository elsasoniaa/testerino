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
