
 1. api_service.dart
📄 Path: lib/app/services/api_service.dart

This helps centralize all HTTP requests so you don’t repeat code in each controller.

import 'dart:convert';
import 'package:http/http.dart' as http;

class ApiService {
  static final _headers = {
    'Content-Type': 'application/json',
    'Accept': 'application/json',
  };

  static Future<dynamic> post(String url, Map<String, dynamic> body) async {
    final response = await http.post(
      Uri.parse(url),
      headers: _headers,
      body: jsonEncode(body),
    );

    return _handleResponse(response);
  }

  static Future<dynamic> get(String url) async {
    final response = await http.get(
      Uri.parse(url),
      headers: _headers,
    );

    return _handleResponse(response);
  }

  static dynamic _handleResponse(http.Response response) {
    final data = jsonDecode(response.body);
    if (response.statusCode >= 200 && response.statusCode < 300) {
      return data;
    } else {
      throw Exception(data['error'] ?? 'API Error');
    }
  }
}




____&&&&&________&&&&&&-&&&__________&&&&-&______&&&&_______&&&&____

model.dart
class Note {
  String? id;
  String title;
  String content;

  Note({this.id, required this.title, required this.content});

  factory Note.fromJson(Map<String, dynamic> json) => Note(
    id: json['_id'],
    title: json['title'],
    content: json['content'],
  );

  Map<String, dynamic> toJson() => {
    'title': title,
    'content': content,
  };
}

API.dart
import 'dart:convert';
import 'package:http/http.dart' as http;
import '../models/note.dart';

class NoteApi {
  static const String baseUrl = 'http://10.0.2.2:5000/api/notes';

  static Future<List<Note>> fetchNotes() async {
    final res = await http.get(Uri.parse(baseUrl));
    return (jsonDecode(res.body) as List).map((json) => Note.fromJson(json)).toList();
  }

  static Future<bool> addNote(Note note) async {
    final res = await http.post(
      Uri.parse(baseUrl),
      headers: {'Content-Type': 'application/json'},
      body: jsonEncode(note.toJson()),
    );
    return res.statusCode == 201;
  }

  static Future<bool> deleteNote(String id) async {
    final res = await http.delete(Uri.parse('$baseUrl/$id'));
    return res.statusCode == 200;
  }

  static Future<bool> updateNote(Note note) async {
    final res = await http.put(
      Uri.parse('$baseUrl/${note.id}'),
      headers: {'Content-Type': 'application/json'},
      body: jsonEncode(note.toJson()),
    );
    return res.statusCode == 200;
  }
}



homepage.dart

import 'package:flutter/material.dart';
import '../models/note.dart';
import '../services/note_api.dart';

class HomeScreen extends StatefulWidget {
  const HomeScreen({super.key});

  @override
  State<HomeScreen> createState() => _HomeScreenState();
}

class _HomeScreenState extends State<HomeScreen> {
  List<Note> notes = [];

  @override
  void initState() {
    super.initState();
    loadNotes();
  }

  void loadNotes() async {
    notes = await NoteApi.fetchNotes();
    setState(() {});
  }

  void deleteNote(String id) async {
    await NoteApi.deleteNote(id);
    loadNotes();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('My Notes')),
      body: ListView.builder(
        itemCount: notes.length,
        itemBuilder: (_, index) {
          final note = notes[index];
          return ListTile(
            title: Text(note.title),
            subtitle: Text(note.content),
            trailing: IconButton(
              icon: Icon(Icons.delete, color: Colors.red),
              onPressed: () => deleteNote(note.id!),
            ),
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () => Navigator.pushNamed(context, '/add').then((_) => loadNotes()),
        child: Icon(Icons.add),
      ),
    );
  }
}
