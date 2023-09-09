## Troubleshooting

Following APIs that can be used from a tool such as POSTMAN to troubleshoot GIN.

**IMPORTANT NOTE 1** : *REST requests to create service instances of models must include following header.*

  ```sh
  Content-Type:application/json
  ```
	
- To get all models from database :
  
  ```sh
  GET https://{NAME_OF_AWS_INSTANCE}-apisix-gateway.{DOMAIN_NAME}/compiler/v1/db/models

  e.g https://dcaf-cmts-demo-apisix-gateway.cci-dev.com/compiler/v1/db/models
  ```
- To get deployable models from the database :
  
  ```sh
  GET https://{NAME_OF_AWS_INSTANCE}-apisix-gateway.{DOMAIN_NAME}/compiler/v1/db/models/deployablemodels
  
  e.g https://cci-server-2-apisix-gateway.cci-dev.com/compiler/v1/db/models/deployablemodels
  ```

- To get all models from database with metadata :
  
  ```sh
  GET https://{NAME_OF_AWS_INSTANCE}-apisix-gateway.{DOMAIN_NAME}/compiler/v1/db/models/metadata

  e.g https://dcaf-cmts-demo-apisix-gateway.cci-dev.com/compiler/v1/db/models/metadata
  ```

- To get specific TOSCA model data :
  
  ```sh
  GET https://{NAME_OF_AWS_INSTANCE}-apisix-gateway.{DOMAIN_NAME}/compiler/v1/db/models/{mainServiceTemplateName}

  e.g https://dcaf-cmts-demo-apisix-gateway.cci-dev.com/compiler/v1/db/models/dcaf_service
  ```

- To get nodeTemplates from DB based on substitute directive :
  
  ```sh
  GET https://{NAME_OF_AWS_INSTANCE}-apisix-gateway.{DOMAIN_NAME}/compiler/v1/db/models/substitute/{nodeTypeName}

  e.g  https://dcaf-cmts-demo-apisix-gateway.cci-dev.com/compiler/v1/db/models/substitute/gin.nodes.MetricsServer
  ```

- To get nodeTemplates from DB based on a select directive :
  
  ```sh
  GET https://{NAME_OF_AWS_INSTANCE}-apisix-gateway.{DOMAIN_NAME}/compiler/v1/db/models/select/{nodeTypeName}

   e.g  https://dcaf-cmts-demo-apisix-gateway.cci-dev.com/compiler/v1/db/models/select/k8s:Cluster
  ```

- To get nodeTemplates from model :
  
  ```sh
  GET https://{NAME_OF_AWS_INSTANCE}-apisix-gateway.{DOMAIN_NAME}/compiler/v1/db/models/{mainServiceTemplateName}/nodetemplates

  e.g.  https://dcaf-cmts-demo-apisix-gateway.cci-dev.com/compiler/v1/db/models/dcaf_service/nodetemplates
  ```

- To get substitution nodes from model :
  
  ```sh
  GET https://{NAME_OF_AWS_INSTANCE}-apisix-gateway.{DOMAIN_NAME}/compiler/v1/db/models/{mainServiceTemplateName}/abstract

  e.g.  https://dcaf-cmts-demo-apisix-gateway.cci-dev.com/compiler/v1/db/models/dcaf_service/abstract
  ```

- To find dangling requirements of a given model :
  
  ```sh
  GET https://{NAME_OF_AWS_INSTANCE}-apisix-gateway.{DOMAIN_NAME}/compiler/v1/db/models/{mainServiceTemplateName}/dangling_requirements

  e.g.  https://dcaf-cmts-demo-apisix-gateway.cci-dev.com/compiler/v1/db/models/dcaf_service/dangling_requirements
  ```
  
- To get all instances from database :
  
  ```sh
  GET https://{NAME_OF_AWS_INSTANCE}-apisix-gateway.{DOMAIN_NAME}/so/v1/instances

   e.g.  https://dcaf-cmts-demo-apisix-gateway.cci-dev.com/so/v1/instances
  ```

- To get specific instance from database :
  
  ```sh
  GET https://{NAME_OF_AWS_INSTANCE}-apisix-gateway.{DOMAIN_NAME}/so/v1/instances/{name}

  e.g https://cci-server-2-apisix-gateway.cci-dev.com/so/v1/instances/cmts1
  ```  
- To get all instances with deployedInstances from database :
  
  ```sh
  GET https://{NAME_OF_AWS_INSTANCE}-apisix-gateway.{DOMAIN_NAME}/so/v1/instances/deployedInstances
  
  e.g https://cci-server-2-apisix-gateway.cci-dev.com/so/v1/instances/deployedInstances
  ```

- To get status of an specific instance
  
  ```sh
  GET https://{NAME_OF_AWS_INSTANCE}-apisix-gateway.{DOMAIN_NAME}/so/v1/instances/{name}/status
  
  e.g https://cci-server-2-apisix-gateway.cci-dev.com/so/v1/instances/cmts1/status
  ```

- To get all policies of an specific instance
  
  ```sh
  GET https://{NAME_OF_AWS_INSTANCE}-apisix-gateway.{DOMAIN_NAME}/so/v1/instances/{name}/policies
  
  e.g https://cci-server-2-apisix-gateway.cci-dev.com/so/v1/instances/cmts1/policies
  ```
        
- To compile model from database :
  
  ```sh
  POST https://{NAME_OF_AWS_INSTANCE}-apisix-gateway.{DOMAIN_NAME}/compiler/v1/model/compile
  
  {
  "url": "path of csar",
  "resolve": true,
  "coerce": false,
  "quirks": [
  "data_types.string.permissive"],
  "output": "./Sample-dgraph-clout.json",
  "inputs": {
    "Sample_Input1": "Value1",
    "Sample_Input2": "Value2"
  },
  "inputsUrl": ""
  }
  
  e.g  https://cci-server-2-apisix-gateway.cci-dev.com/compiler/v1/model/compile

  
  {
  "url": "/opt/app/csars/dcaf-cmts.csar",
  "resolve": true,
  "coerce": false,
  "quirks": [
  "data_types.string.permissive"
   ],
  "output": "dcaf-cmts-clout.json",
  "inputs": "",
  "inputsUrl": "",
  "force": true
  }
  
  ```
- To save model in database :

  ```sh
  POST https://{NAME_OF_AWS_INSTANCE}-apisix-gateway.{DOMAIN_NAME}/compiler/v1/model/db/save

  {
  "url": "{path of csar}",
  "resolve": true,
  "coerce": false,
  "quirks": [
    "data_types.string.permissive"
  ],
  "output": "./Sample-dgraph-clout.json",
  "inputs": {
    "Sample_Input1": "Value1",
    "Sample_Input2": "Value2"
  },
  "inputsUrl": ""
  }

  e.g. https://cci-server-2-apisix-gateway.cci-dev.com/compiler/v1/model/db/save
  {
  "url": "/opt/app/csars/dcaf-cmts.csar",
  "resolve": true,
  "coerce": false,
  "quirks": [
  "data_types.string.permissive"
   ],
  "output": "dcaf-cmts-clout.json",
  "inputs": "",
  "inputsUrl": "",
  "force": true
  }
  ```

- To delete a model from database :

  ```sh
  DELETE https://{NAME_OF_AWS_INSTANCE}-apisix-gateway.{DOMAIN_NAME}/compiler/v1/model/db/{MODEL_NAME}
  {
    "namespace": "{MODEL_SERVICE_URL}",
    "version": "tosca_simple_yaml_1_3",
    "includeTypes": true
  }

  e.g.
   DELETE https://dcaf-cmts-demo-apisix-gateway.cci-dev.com/compiler/v1/model/db/dcaf_service
  {
    "namespace": "zip:file:/opt/app/csars/dcaf-cmts.csar!/dcaf_service.yaml",
    "version": "tosca_simple_yaml_1_3",
    "includeTypes": true
  }
  ```
- To create instance:

  ```sh
  POST https://{NAME_OF_AWS_INSTANCE}-apisix-gateway.{DOMAIN_NAME}/so/v1/instances/createInstance
  
  {
    "name": "{instance-name}",
    "output": "dcaf-cmts.json",
    "generate-workflow": true,
    "execute-workflow": true,
    "list-steps-only": false,
    "execute-policy": true,
    "inputs": {
        "input1": {
            "value1"
        },
        
        "input2": {
            "value2"
        }
    },
    "inputsUrl": "",
    "service": "{models csar path}"
  }

 
   e.g POST https://cci-server-2-apisix-gateway.cci-dev.com/so/v1/instances/createInstance

  {
    "name": "dcaf91",
    "output": "dcaf-cmts.json",
    "generate-workflow": true,
    "execute-workflow": true,
    "list-steps-only": false,
    "execute-policy": true,
    "inputs": {
        "dcaf-input-resource": {
            "k8scluster_name": "dcaf"
        },
        "cluster": {
            "cluster-input-resource": {
                "cluster_name": "dcaf"
            }
        },
        "ves-collector": {
            "k8scluster_name": "dcaf"
        }
    },
    "inputsUrl": "",
    "service": "zip:/opt/app/csars/dcaf-cmts.csar!/dcaf_service.yaml"
  }
  ```

- To execute workflow steps of a model which has already been saved in the database :

  ```sh
  POST https://{NAME_OF_AWS_INSTANCE}-apisix-gateway.{DOMAIN_NAME}/so/v1/instances/{INSTANCE_NAME}/workflows/deploy
  {
    "list-steps-only": false,
    "execute-policy": true
  }

    POST https://dcaf-cmts-demo-apisix-gateway.cci-dev.com/so/v1/instances/dcaf1/workflows/deploy
  {
    "list-steps-only": false,
    "execute-policy": true
  }
  ```
