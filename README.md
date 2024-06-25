# flutter_application_10

A new Flutter project.

## Getting Started

This project is a starting point for a Flutter application.

A few resources to get you started if this is your first Flutter project:

- [Lab: Write your first Flutter app](https://docs.flutter.dev/get-started/codelab)
- [Cookbook: Useful Flutter samples](https://docs.flutter.dev/cookbook)

For help getting started with Flutter development, view the
[online documentation](https://docs.flutter.dev/), which offers tutorials,
samples, guidance on mobile development, and a full API reference.

# Extract Widget

Extract widget adalah metode pemecahan sebuah widget agar lebih efesian, optimal dan reusealble atau dapat digunakan ulang kembali. extract widget dapat dilakukan dengan fokus ke widget yang akan kita extract dengan cara refactor extract widget. extract widget memudahkan kita dalam membuat sebuah tampilan menjadi kecil - kecil seperti beberapa component yang akan kita gunakan kembali atua reuseable. extract widget sangat penting agar code kita tidak terlalu banyak dalam kondisi code yang berulang.

```dart
import 'package:flutter/material.dart';
import 'package:faker/faker.dart';

void main(List<String> args) {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  final faker = Faker();
  final String imageUrl = "https://picsum.photos/id";

  MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        backgroundColor: Colors.grey[200],
        appBar: AppBar(
          title: const Text('Extract widgets'),
        ),
        body: ListView.builder(
          itemCount: faker.randomGenerator.integer(20),
          itemBuilder: (context, index) {
            return ChatItem(
              imageUrl:
                  "$imageUrl/${faker.randomGenerator.integer(100).toString()}/200/300",
              name: faker.person.name(),
              time: faker.date.justTime(),
              message: faker.lorem.sentence(),
              countMessage: faker.randomGenerator.integer(100).toString(),
            );
          },
        ),
        floatingActionButton: FloatingActionButton(
          onPressed: () {},
          child: const Icon(
            Icons.add_comment_rounded,
          ),
          backgroundColor: Colors.lightGreenAccent.shade700,
        ),
        bottomNavigationBar: BottomNavigationBar(
          type: BottomNavigationBarType.fixed,
          items: const [
            BottomNavigationBarItem(
              icon: Icon(Icons.message),
              label: 'Chat',
            ),
            BottomNavigationBarItem(
              icon: Icon(Icons.track_changes_outlined),
              label: 'Pembaruan',
            ),
            BottomNavigationBarItem(
              icon: Icon(Icons.people_outline_outlined),
              label: 'Komunitas',
            ),
            BottomNavigationBarItem(
              icon: Icon(Icons.phone_outlined),
              label: 'Panggilan',
            ),
          ],
        ),
      ),
    );
  }
}

/*
	disini extract widget yang kita lakukan untuk membuat widget yang akan digunakan
	di class MyApp, extract widget lebih bagus membangun constructor yang berisi properti atau field
	yang akan digunakan di dalam extract widget agar lebih dinamis
*/
class ChatItem extends StatelessWidget {
  final String? name;
  final String? message;
  final String? time;
  final String? countMessage;
  final String? imageUrl;

  const ChatItem({
    super.key,
    required this.name,
    required this.message,
    required this.time,
    required this.countMessage,
    required this.imageUrl,
  });

  @override
  Widget build(BuildContext context) {
    return ListTile(
      leading: CircleAvatar(
        backgroundImage: NetworkImage(imageUrl!),
      ),
      title: Text(
        name!,
      ),
      subtitle: Text(
        message!,
        maxLines: 1,
        overflow: TextOverflow.ellipsis,
      ),
      trailing: Column(
        children: [
          Text(time!,
              style: TextStyle(color: Colors.lightGreenAccent.shade700)),
          CircleAvatar(
            backgroundColor: Colors.lightGreenAccent.shade700,
            maxRadius: 15,
            child: Text(countMessage!),
          ),
        ],
      ),
    );
  }
}
```
