# EnableDepthMask

Habilita a escrita no Z-buffer.

## Assinatura

```lua
EnableDepthMask() -> void
```

## Parâmetros

Nenhum.

## Retorno

`nil` - Esta função não retorna valor.

## Uso

Habilita a escrita no Z-buffer, permitindo que objetos atualizem o buffer de profundidade. Use quando quiser que objetos afetem o depth buffer.

## Exemplos

### Configuração de Depth

```lua
function BridgeFunction_OnInterfaceRender()
    -- Habilitar escrita no Z-buffer
    EnableDepthMask()
    
    -- Renderizar objetos que devem afetar o depth buffer
    RenderBitmap(objectTexture, 100, 100, 200, 200, 0, 0, 1, 1, false, false, 1.0)
end
```

## Notas Importantes

1. **Z-buffer**: Controla a escrita no buffer de profundidade
2. **Use com objetos 3D**: Ideal para objetos que devem interagir com o depth buffer
3. **Performance**: Pode ter impacto na performance dependendo do uso
4. **Combine com DisableDepthTest**: Use junto com outras funções de depth para controle completo

## Funções Relacionadas

- [DisableDepthMask](DisableDepthMask.md) - Desabilita escrita no Z-buffer
- [DisableDepthTest](DisableDepthTest.md) - Desabilita teste de profundidade
- [Sistema de Renderização](../06-Sistema-Renderizacao.md) - Documentação completa do sistema de renderização

