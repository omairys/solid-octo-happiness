# 🚀 Guía Rápida - Conciliador Financiero

## ✅ Estado del Sistema

Servicios esperados:

| Servicio | URL | Estado |
|----------|-----|--------|
| **n8n** | http://localhost:5678 | 🟢 Activo |
| **PostgreSQL** | localhost:5432 | 🟢 Activo |

---

## ⚙️ Paso 1: Levantar servicios

```bash
docker compose up -d
```

Verifica estado:

```bash
docker compose ps
```

---

## 🤖 Paso 2: Crear un flujo basico en n8n

1. Abre http://localhost:5678
2. Si es la primera vez, crea tu cuenta de administrador
3. Haz clic en **"Create new workflow"**
4. Agrega un nodo **Webhook**:
   - **HTTP Method**: `POST`
   - **Path**: `webhook-test`
   - **Authentication**: `None`
5. Haz clic en **"Listen for Test Event"**

---

## 🔧 Comandos utiles

### Ver logs en tiempo real
```bash
docker compose logs -f
```

### Ver logs solo de n8n
```bash
docker compose logs -f n8n
```

### Reiniciar servicios
```bash
docker compose restart
```

### Detener todo
```bash
docker compose down
```

---

## 📚 Documentacion

- [n8n Docs](https://docs.n8n.io/)
- [README Principal](./README.md)
