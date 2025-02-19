# insurance-core-platform
Plataforma white-label para seguros
/insurance-core-platform
├──📁 n8n-flows
│   └── Fluxo_Mestre_N8N_Agentes.json
├──📁 flutter-apps
│   ├── app-filmes-design-thn7dy
│   └── delivery-app-n6yyak  
├──📄 README.md
└──📄 .gitignore
# Insurance Core Platform 🏦

![Badges](https://img.shields.io/badge/Stack-FlutterFlow%20%7C%20n8n%20%7C%20Xano-blueviolet)

Plataforma white-label para operações de seguros digitais implementada para [Olga.ai](https://olga-ai.com)

## Funcionalidades Principais
- ✅ Emissão automática de apólices
- 💳 Integração com meios de pagamento
- 🤖 Automatização de fluxos com n8n
- 📱 Apps mobile prontos (FlutterFlow)

## Como Usar
1. Clone o repositório:
```bash
git clone https://github.com/seu-usuario/insurance-core-platform.git
```

2. Importe fluxos no n8n:
```json
{
  "name": "[F. N8N] Case 1. 80/20 [Modelo]",
  "nodes": [
    {
      "parameters": {
        "conditions": {
          "options": {
            "caseSensitive": true,
            "leftValue": "",
            "typeValidation": "strict"
          },
          "conditions": [
            {
              "id": "24aa4532-80db-4c1e-977a-0036b82a8e5f",
              "leftValue": "={{ $json.body.isEdit }}",
              "rightValue": "false",
              "operator": {
                "type": "boolean",
                "operation": "false",
                "singleValue": true
              }
            },
            {
              "id": "204f54b0-e3ed-4ff4-8302-8c20d3b8aa78",
              "leftValue": "={{ $json.body.isGroup }}",
              "rightValue": "",
              "operator": {
                "type": "boolean",
                "operation": "false",
                "singleValue": true
              }
            },
            {
              "id": "130cc493-a17a-4cc1-955b-816799583076",
              "leftValue": "={{ $json.body.isNewsletter }}",
              "rightValue": "",
              "operator": {
                "type": "boolean",
                "operation": "false",
                "singleValue": true
              }
            },
            {
              "id": "c51986d9-f347-4198-89bb-9e4cd0f021c9",
              "leftValue": "={{ $json.body.broadcast }}",
              "rightValue": "",
              "operator": {
                "type": "boolean",
                "operation": "false",
                "singleValue": true
              }
            },
            {
              "id": "ac9c4286-34d7-4058-9bbb-985bd9c2b6e7",
              "leftValue": "={{ $json.body.fromApi }}",
              "rightValue": "",
              "operator": {
                "type": "boolean",
                "operation": "false",
                "singleValue": true
              }
            }
          ],
          "combinator": "and"
        },
        "options": {}
      },
      "id": "878c256a-d1cb-4a93-88ed-a1eeb2d25f7e",
      "name": "Filtro Inicial Mensagens",
      "type": "n8n-nodes-base.filter",
      "typeVersion": 2.1,
      "position": [
        680,
        280
      ]
    },
    {
      "parameters": {
        "model": "gpt-4o-mini",
        "options": {}
      },
      "id": "69cfcfbb-1dde-4641-911e-882acae83817",
      "name": "OpenAI Chat Model",
      "type": "@n8n/n8n-nodes-langchain.lmChatOpenAi",
      "typeVersion": 1,
      "position": [
        1760,
        480
      ],
      "credentials": {
        "openAiApi": {
          "id": "zK1bsB4i4ETFQdEq",
          "name": "OpenAI NoCode StartUp"
        }
      }
    },
    {
      "parameters": {},
      "id": "677bfbdc-507c-45b7-8143-ad753dab19d4",
      "name": "No Operation, do nothing",
      "type": "n8n-nodes-base.noOp",
      "typeVersion": 1,
      "position": [
        2320,
        279
      ]
    },
    {
      "parameters": {
        "content": "## Gatilho\n",
        "height": 235.12669720206657,
        "width": 229.01065895241982
      },
      "id": "be8d7680-4e61-4175-967b-c95d43ebe075",
      "name": "Sticky Note",
      "type": "n8n-nodes-base.stickyNote",
      "typeVersion": 1,
      "position": [
        380,
        220
      ]
    },
    {
      "parameters": {
        "content": "## Gestão de usuários e conversas\n",
        "height": 353.12603949580904,
        "width": 1071.701076784341,
        "color": 4
      },
      "id": "55611477-8d9f-4b6a-9d46-6a44956874c6",
      "name": "Sticky Note1",
      "type": "n8n-nodes-base.stickyNote",
      "typeVersion": 1,
      "position": [
        620,
        220
      ]
    },
    {
      "parameters": {
        "assignments": {
          "assignments": [
            {
              "id": "69f6217f-9063-423f-abf4-e94f6b70f94e",
              "name": "ClienteNome",
              "value": "={{ $('Webhook').item.json.body.senderName }}",
              "type": "string"
            },
            {
              "id": "9f488c5c-0b3b-48e9-87b1-5a22d513d1ec",
              "name": "ClienteTelefone",
              "value": "={{ $('Webhook').item.json.body.phone }}",
              "type": "string"
            },
            {
              "id": "1ae1a51c-00cb-47f9-8dc8-5a05c66fc0c8",
              "name": "Mensagem",
              "value": "={{ $('Webhook').item.json.body.text.message }}",
              "type": "string"
            }
          ]
        },
        "includeOtherFields": "=",
        "options": {}
      },
      "id": "b65a5ecd-36c0-421b-b442-51413476f3a4",
      "name": "Simplificação de Dados",
      "type": "n8n-nodes-base.set",
      "typeVersion": 3.4,
      "position": [
        880,
        280
      ]
    },
    {
      "parameters": {
        "sessionIdType": "customKey",
        "sessionKey": "={{ $('Simplificação de Dados').item.json.ClienteTelefone }}",
        "contextWindowLength": 0
      },
      "id": "405b559c-0e35-4afe-99d6-64e471bc1bb6",
      "name": "Window Buffer Memory",
      "type": "@n8n/n8n-nodes-langchain.memoryBufferWindow",
      "typeVersion": 1.2,
      "position": [
        1900,
        480
      ]
    },
    {
      "parameters": {
        "conditions": {
          "options": {
            "caseSensitive": true,
            "leftValue": "",
            "typeValidation": "strict"
          },
          "conditions": [
            {
              "id": "3419c30f-4400-401b-bf40-db1579507f96",
              "leftValue": "={{ $json.id }}",
              "rightValue": "",
              "operator": {
                "type": "number",
                "operation": "exists",
                "singleValue": true
              }
            }
          ],
          "combinator": "and"
        },
        "options": {}
      },
      "id": "8fda01c5-9464-4562-ac2f-8f3d157d5da7",
      "name": "Cliente Existe?",
      "type": "n8n-nodes-base.if",
      "typeVersion": 2.1,
      "position": [
        1240,
        280
      ],
      "alwaysOutputData": false
    },
    {
      "parameters": {
        "method": "POST",
        "url": "https://api.z-api.io/instances/{SUA-INSTANCIA}/token/{SEU-TOKEN}/send-text",
        "authentication": "genericCredentialType",
        "genericAuthType": "httpHeaderAuth",
        "sendBody": true,
        "bodyParameters": {
          "parameters": [
            {
              "name": "phone",
              "value": "={{ $('Simplificação de Dados').item.json.ClienteTelefone }}"
            },
            {
              "name": "message",
              "value": "={{ $json.output }}"
            }
          ]
        },
        "options": {}
      },
      "id": "dfed7301-bb6a-4f09-906a-57b59b1eb774",
      "name": "(Z-API) Enviar Mensagem",
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.2,
      "position": [
        2180,
        280
      ],
      "credentials": {
        "httpHeaderAuth": {
          "id": "18ZooK5mNEEU3JoS",
          "name": "Z-API Security Token"
        }
      }
    },
    {
      "parameters": {},
      "id": "136ef475-b55c-474e-b873-a2019bfd05bc",
      "name": "Merge",
      "type": "n8n-nodes-base.merge",
      "typeVersion": 3,
      "position": [
        1540,
        280
      ]
    },
    {
      "parameters": {
        "content": "## Agente IA",
        "height": 394.92781780142946,
        "width": 358.3001137069198,
        "color": 5
      },
      "id": "a04994b9-56ce-468b-b077-ca446610e10c",
      "name": "Sticky Note2",
      "type": "n8n-nodes-base.stickyNote",
      "typeVersion": 1,
      "position": [
        1720,
        220
      ]
    },
    {
      "parameters": {
        "content": "## Respondendo WhatsApp",
        "height": 272.19228980427147,
        "width": 427.92776086093977,
        "color": 7
      },
      "id": "eb2dcc9e-fd0d-42de-b63e-3bd2bb316624",
      "name": "Sticky Note3",
      "type": "n8n-nodes-base.stickyNote",
      "typeVersion": 1,
      "position": [
        2100,
        220
      ]
    },
    {
      "parameters": {
        "agent": "conversationalAgent",
        "promptType": "define",
        "text": "={{ $('Simplificação de Dados').item.json.Mensagem }}",
        "options": {
          "systemMessage": "Você é o melhor vendedor do mundo.\nEm toda interação tente vender algo relacionado ao que usuário falou, de forma engraçada e persuasiva para o usuário."
        }
      },
      "id": "9d54a8e7-74f8-48f5-9b74-8beda0ed97bd",
      "name": "AI Agent",
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 1.6,
      "position": [
        1760,
        280
      ]
    },
    {
      "parameters": {
        "operation": "get",
        "tableId": "usuarios",
        "filters": {
          "conditions": [
            {
              "keyName": "whatsapp",
              "keyValue": "={{ $json.ClienteTelefone }}"
            }
          ]
        }
      },
      "id": "3d71a1c1-1216-45b4-a86e-60ef2a2491b7",
      "name": "Encontrar Cliente",
      "type": "n8n-nodes-base.supabase",
      "typeVersion": 1,
      "position": [
        1080,
        280
      ],
      "alwaysOutputData": true,
      "credentials": {
        "supabaseApi": {
          "id": "c3ppibhd1RX2rXji",
          "name": "Supabase Neto"
        }
      }
    },
    {
      "parameters": {
        "tableId": "usuarios",
        "fieldsUi": {
          "fieldValues": [
            {
              "fieldId": "nome",
              "fieldValue": "={{ $('Simplificação de Dados').item.json.ClienteNome }}"
            },
            {
              "fieldId": "whatsapp",
              "fieldValue": "={{ $('Simplificação de Dados').item.json.ClienteTelefone }}"
            }
          ]
        }
      },
      "id": "07377bc0-4128-48a2-b89a-862ced211607",
      "name": "Criar Cliente",
      "type": "n8n-nodes-base.supabase",
      "typeVersion": 1,
      "position": [
        1380,
        380
      ],
      "credentials": {
        "supabaseApi": {
          "id": "c3ppibhd1RX2rXji",
          "name": "Supabase Neto"
        }
      }
    },
    {
      "parameters": {
        "httpMethod": "POST",
        "path": "bc978142-377f-4daf-b31e-3390dc1be1df",
        "options": {}
      },
      "id": "0b7167bc-3c3b-4a05-a915-4a5a4da5395a",
      "name": "Webhook",
      "type": "n8n-nodes-base.webhook",
      "typeVersion": 2,
      "position": [
        440,
        280
      ],
      "webhookId": "bc978142-377f-4daf-b31e-3390dc1be1df"
    }
  ],
  "pinData": {},
  "connections": {
    "Filtro Inicial Mensagens": {
      "main": [
        [
          {
            "node": "Simplificação de Dados",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "OpenAI Chat Model": {
      "ai_languageModel": [
        [
          {
            "node": "AI Agent",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "Simplificação de Dados": {
      "main": [
        [
          {
            "node": "Encontrar Cliente",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Window Buffer Memory": {
      "ai_memory": [
        [
          {
            "node": "AI Agent",
            "type": "ai_memory",
            "index": 0
          }
        ]
      ]
    },
    "Cliente Existe?": {
      "main": [
        [
          {
            "node": "Merge",
            "type": "main",
            "index": 0
          }
        ],
        [
          {
            "node": "Criar Cliente",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "(Z-API) Enviar Mensagem": {
      "main": [
        [
          {
            "node": "No Operation, do nothing",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Merge": {
      "main": [
        [
          {
            "node": "AI Agent",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "AI Agent": {
      "main": [
        [
          {
            "node": "(Z-API) Enviar Mensagem",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Encontrar Cliente": {
      "main": [
        [
          {
            "node": "Cliente Existe?",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Criar Cliente": {
      "main": [
        [
          {
            "node": "Merge",
            "type": "main",
            "index": 1
          }
        ]
      ]
    },
    "Webhook": {
      "main": [
        [
          {
            "node": "Filtro Inicial Mensagens",
            "type": "main",
            "index": 0
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {
    "executionOrder": "v1",
    "saveManualExecutions": true,
    "callerPolicy": "workflowsFromSameOwner",
    "executionTimeout": 60
  },
  "versionId": "e382a9bb-e698-47cf-9e42-2deabddf4707",
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "c2cf0571d78da189c5916e815dd57e9fc54736be5196d86f4402a03a1245164c"
  },
  "id": "Q7L8IxuWKoeJVk7w",
  "tags": [
    {
      "createdAt": "2024-09-14T16:51:28.535Z",
      "updatedAt": "2024-09-14T16:51:28.535Z",
      "id": "690f47PmWdvT1q122",
      "name": "Arthur Musa"
    }
  ]
}

**Projetos Relacionados:**
- [App de Filmes](https://app.flutterflow.io/project/app-filmes-design-thn7dy)
- [Sistema de Cursos](https://app.flutterflow.io/project/supabase-app-de-cursos-iv9juo)
