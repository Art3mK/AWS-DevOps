# Cloudformation (cfn)

- BeanStalk uses cfn
- automatic rollback on error is enable by default
- you are charged for errors
- cloudformation is free
- stacks can wait for apps using the `WaitCondition`
- `Fn:GetAtt` to output data
- IAM Role Creation and Assigment is also supported

## cfn build blocks
- stack
- template
- stack policy (statement which governs what can be changed and by who)

### Templates anatomy

- *params*
- *mappings* (hashes)
- resources
    ```
    actual resrouces
    ```
- *outputs*

### Parameters

#### Types

- String
- Number
- List
- CSV list
- AWS specific types, `AWS::EC2::KeyPair::KeyName`, `AWS::EC2::AvailabilityZone::Name`
- SSM Parameter Types (doesn't currently support the SecureString Systems Manager parameter type)

#### properties

- maximum of 60 parameters in template
- params can have default values
- allowed values (predefined values)
- allowed (regexp) pattern]
- min & max for numbers
- min & man lenght for strings
- `NoEcho` - mask the parameter value when a call is made that describes the stack
- use `Ref` to reference a parameter, can reference own params and outputs
- supports grouping and sorting via `AWS::CloudFormation::Interface` metadata key

### Resources

- mandatory section
- logical ID (friendly name) is mandatory

## Links

- https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/parameters-section-structure.html