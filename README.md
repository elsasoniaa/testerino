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
