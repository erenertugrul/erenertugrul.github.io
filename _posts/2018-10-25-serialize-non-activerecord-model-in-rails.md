---
layout: post
title:  "Serialize Non-ActiveRecord Model Using ActiveModel::Serializer in Rails"
date:   2018-10-25 11:30:09 +0900
comments: true
tags:
- programming
---

Recently I've been working in backend which connects to another API, you may need to send a specific format of JSON data which is not the same as database resource.

## Create A Serializable Resource
Currently I'm using <a href='https://github.com/rails-api/active_model_serializers/tree/0-10-stable'>active_model_serializers 0.10.0</a>. From the documentation we know `ActiveModel::Serializer` wraps a serializable resource, to create a serializable resource we need to create a plain old Ruby object inherits `ActiveModelSerializers::Model`, then create a corresponding serializer.

For example:
```rb
class MyModel < ActiveModelSerializers::Model
  def initialize(title:, body:)
    @title = title
    @body = body
  end

  def converted_body
    # do something
  end
end
```

```rb
class MyModelSerializer < ActiveModelSerializers::Serializer
  attributes :converted_body
end
```

## Handling Nested JSON
You can use `has_many`, `has_one` method in `ActiveModel::Serializer` to handle nested json, although it doesn't mean the same with Rails model relations.

For example:
```rb
class MyModel < ActiveModelSerializers::Model
  def initialize(object: object)
    @title = title
    @body = body
  end

  def 

  def related_models
    related_models.map do |related_model|
      RelatedModel.new(related_model: related_model)
    end
  end
end
```

```rb
class MyModelSerializer < ActiveModelSerializers::Serializer
  has_many :related_models
end
```
`ActiveModelSerializers::Serializer` will automatically look for a serializer named `RelatedModelSerializer`.

## Reference
Find more explainations in   https://github.com/rails-api/active_model_serializers/tree/0-10-stable#what-does-a-serializable-resource-look-like


