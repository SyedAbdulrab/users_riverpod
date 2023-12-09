# users api in River

> This is a practice app in which I am familiarizing myself with the concepts of Using flutter riverpod and managing application wide state data that I fetch from an API first.

key moments:
```
final userProvider = Provider<ApiServices>(ref=>ApiServices());

final userDataProvider = FutureProvider<List<UserModels>>((ref)async{
      return ref.watch(userProvider).getUsers()
})
```
-- Note:- Every flutter riverpod application should have the provider scope i.e the runApp(ProviderScope(child: myApp())), otherwise you wont be able to access the shared state.


Now to access the shared state inside of your application:

make a statless widget and make it extend the *CONSUMER STATE WIDGET* class

then:-
```
final _data = ref.watch(userDataProvider);

Scaffold(
body: _data.when(
data: (_data){
List<UserModel> userList = _data.map(e=>e).toList();
return ListView.builder(
itemCount: userList.length,
ItemBuilder: (_,index){
  return Text(userList\[index].username)
}
)
},
error:(err, s) => Text(err.toString()),
loading:()=>CircularProgressIndicator(),
)
)

