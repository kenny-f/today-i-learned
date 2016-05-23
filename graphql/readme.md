## Mapping source key to something else
When an api or database returns an object with a key has an unsupported 
character (eg `$type`) or you just want to give it a different name. 
You can use the `resolve` function like so: 

Say you get the following response from an api
```
{
  $type: 'some type',
  name: 'Iron Man'
}
```

In your object definition you can do: 
```
export default new GraphQLObjectType({
  name: 'Some name',
  fields: () => ({
    type: {
      type: GraphQLString,
      resolve(obj) {
        return obj.$type;
      },
    },
    name: { type: GraphQLString, },
  }),
});

```

The argument to the resolve method is object that comes from the api/database.

This is also useful to do any mapping that is required from the source
to your desired output. For example:
```
export default new GraphQLObjectType({
  name: 'Some name',
  fields: () => ({
    fullname: {
     type: GraphQLString,
     resolve(obj) {
             return obj.firstname + ' ' + obj.lastname;
           },
    },
  }),
});
```
