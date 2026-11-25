# Day 17: UI Libraries & Component Frameworks

This day focuses on using professional UI libraries to speed up development while maintaining a high-quality, consistent look and feel.

## 1. Ant Design (AntD)
Ant Design is an enterprise-class UI design language and React UI library. It is widely used for internal tools, dashboards, and complex B2B applications.

### Why use Ant Design?
- **Comprehensive Component Set**: Includes everything from basic buttons to complex tables, date pickers, and form validation.
- **Design System**: Follows a strict design language for consistency.
- **TypeScript Support**: Excellent type definitions.

### Getting Started with AntD
**Installation:**
```bash
npm install antd
```

**Basic Example:**
```jsx
import React from 'react';
import { Button, DatePicker, Space, Table } from 'antd';

const App = () => {
  const columns = [
    { title: 'Name', dataIndex: 'name', key: 'name' },
    { title: 'Age', dataIndex: 'age', key: 'age' },
  ];
  const data = [
    { key: '1', name: 'John Doe', age: 32 },
    { key: '2', name: 'Jane Smith', age: 28 },
  ];

  return (
    <div style={{ padding: '20px' }}>
      <h1>Enterprise Dashboard</h1>
      <Space direction="vertical" style={{ width: '100%' }}>
        <Space>
          <Button type="primary">Primary Button</Button>
          <DatePicker />
        </Space>
        <Table dataSource={data} columns={columns} />
      </Space>
    </div>
  );
};

export default App;
```

## 2. Other Important UI Libraries

### Material UI (MUI)
The most popular React UI library based on Google's Material Design.
- **Best for:** Consumer-facing apps that want a "Google-like" feel.
- **Key Feature:** Highly customizable theme provider.

### Chakra UI
A simple, modular, and accessible component library.
- **Best for:** Rapid prototyping and developers who prefer a "prop-based" styling approach (similar to Tailwind).
- **Example:** `<Box bg="blue.500" color="white" p={4} borderRadius="md">`

### Headless UI / Radix UI
These are "headless" libraries, meaning they provide the **logic and accessibility** but **no styles**.
- **Best for:** When you want full control over the CSS (usually paired with Tailwind CSS).
- **Why?** You get the complex keyboard navigation and ARIA roles for free, but you style it exactly how you want.

## 3. Choosing the Right Library

| Library | Style | Customization | Learning Curve | Best Use Case |
| :--- | :--- | :--- | :--- | :--- |
| **Ant Design** | Enterprise/Clean | Medium | Medium | Admin Panels, B2B, Dashboards |
| **MUI** | Material Design | High | Medium | General Purpose, Consumer Apps |
| **Chakra UI** | Modern/Clean | High | Low | Fast Prototyping, SaaS |
| **Radix/Headless** | None (You style) | Absolute | Medium | Custom Design Systems, High-End UI |
