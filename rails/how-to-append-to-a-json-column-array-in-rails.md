# How to append to a json column array in Rails

Reference: https://gist.github.com/skunkworker/56067edc1f1d4268381c78393e86b6dc

This is copy of the code copied from the link above

Assuming Model is your model and options is a json/jsonb column.
This uses the Postgres json append || operator.
And wraps the option inside an array.
producing [{},{}] multiple hashes inside a top level json array.

It is very important that the hash is [{}] NOT {} as not having the array on the 
outside will cause the hash to replace the contents instead of appending to them.

```
new_option = [{
  name: option_name,
  time: Time.now.iso8601
}].to_json

Model.where(id: model.id).update_all(["options = options || ?::jsonb", new_option])
```
Additional reading
https://stackoverflow.com/questions/42233542/appending-pushing-and-removing-from-a-json-array-in-postgresql-9-5
