✅ 3. validators.dart
📄 Path: lib/app/utils/validators.dart

Reusable validation methods for forms:


class Validators {
  static String? validateEmail(String? value) {
    if (value == null || value.isEmpty) return 'Email is required';
    final emailRegex = RegExp(r'^[^@]+@[^@]+\.[^@]+');
    if (!emailRegex.hasMatch(value)) return 'Enter a valid email';
    return null;
  }

  static String? validatePassword(String? value) {
    if (value == null || value.isEmpty) return 'Password is required';
    if (value.length < 6) return 'Password must be at least 6 characters';
    return null;
  }

  static String? validateName(String? value) {
    if (value == null || value.trim().isEmpty) return 'Name is required';
    return null;
  }
}




Usage in forms:

TextFormField(
  validator: Validators.validateEmail,
)





2. constants.dart
📄 Path: lib/app/utils/constants.dart

This file keeps all hard-coded strings, colors, etc., in one place.
import 'package:flutter/material.dart';

class AppConstants {
  static const appName = "RealWorld Flutter App";

  // Colors
  static const primaryColor = Colors.blue;
  static const accentColor = Colors.orange;

  // URLs
  static const baseUrl = 'https://jsonplaceholder.typicode.com';
  static const loginUrl = 'https://reqres.in/api/login';
  static const postsUrl = '$baseUrl/posts';

  // Dummy user
  static const defaultUserName = "John Doe";
  static const defaultEmail = "john@example.com";
}
