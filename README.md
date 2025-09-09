# edvironassement

A comprehensive full-stack web application for monitoring and managing school payment transactions. Built with modern React frontend and Express.js backend, providing real-time data visualization and filtering capabilities for educational institutions' payment processing needs.

## 🚀 Features

- **Transaction Dashboard**: Complete overview with statistics and filtering
- **School-specific Views**: View transactions filtered by specific schools
- **Transaction Status Checker**: Real-time status checking using custom order IDs
- **Payment Gateway Integration**: Support for PhonePe, GooglePay, Paytm, Razorpay
- **Webhook Processing**: Handle payment gateway callbacks
- **Dark/Light Theme**: Toggle between themes with persistent settings
- **Responsive Design**: Works seamlessly on desktop, tablet, and mobile
- **Advanced Filtering**: Filter by status, school, date range, and search functionality

## 📋 Requirements

- Node.js 20+
- npm or yarn package manager

## 🛠️ Installation & Setup

1. **Clone the repository**
```bash
git clone <repository-url>
cd edviron-payment-dashboard
```

2. **Install dependencies**
```bash
npm install
```

3. **Environment Variables**
Create a `.env` file in the root directory with the following variables:
```env
JWT_SECRET=your-jwt-secret-key
API_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ0cnVzdGVlSWQiOiI2NWIwZTU1MmRkMzE5NTBhOWI0MWM1YmEiLCJJbmRleE9mQXBpS2V5Ijo2LCJpYXQiOjE3MTE2MjIyNzAsImV4cCI6MTc0MzE3OTg3MH0.Rye77Dp59GGxwCmwWekJHRj6edXWJnff9finjMhxKuw
PG_KEY=edvtest01
SCHOOL_ID=65b0e6293e9f76a9694d84b4
```

4. **Start the application**
```bash
npm run dev
```

The application will be available at `http://localhost:5000`

## 🏗️ System Architecture

### Frontend Architecture
- **React with TypeScript**: Component-based architecture
- **shadcn/ui + Tailwind CSS**: Modern, responsive UI components
- **Wouter**: Client-side routing for navigation
- **TanStack Query**: Server state management and caching
- **Theme Provider**: Light/dark mode support

### Backend Architecture
- **Express.js with TypeScript**: RESTful API server
- **JWT Authentication**: Secure token-based authentication
- **In-Memory Storage**: Fast data access for development
- **Webhook Processing**: Handle payment gateway callbacks
- **Comprehensive Error Handling**: Consistent error responses

### Database Schema
The system uses the following main entities:

**Orders Schema**
```javascript
{
  _id: ObjectId,
  school_id: String,
  trustee_id: String,
  student_info: {
    name: String,
    id: String,
    email: String
  },
  gateway_name: String,
  custom_order_id: String
}
```

**Order Status Schema**
```javascript
{
  collect_id: ObjectId, // Reference to Order._id
  order_amount: Number,
  transaction_amount: Number,
  payment_mode: String,
  payment_details: String,
  bank_reference: String,
  payment_message: String,
  status: String, // 'success', 'pending', 'failed'
  error_message: String,
  payment_time: Date
}
```

## 📡 API Endpoints

### Authentication
- `POST /api/auth/login` - User login with JWT token generation

### Payment Operations
- `POST /api/create-payment` - Create new payment request
- `POST /api/webhook` - Process payment gateway webhooks

### Transaction Queries
- `GET /api/transactions` - Get all transactions with filtering
- `GET /api/transactions/school/:schoolId` - Get transactions by school
- `GET /api/transaction-status/:custom_order_id` - Check transaction status

### Dashboard
- `GET /api/dashboard/stats` - Get dashboard statistics

## 🎯 API Usage Examples

### Get All Transactions
```bash
curl -X GET "http://localhost:5000/api/transactions?page=1&limit=10&status=success"
```

### Check Transaction Status
```bash
curl -X GET "http://localhost:5000/api/transaction-status/ORD-1706123456-ABC123"
```

### Create Payment
```bash
curl -X POST "http://localhost:5000/api/create-payment" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer <JWT_TOKEN>" \
  -d '{
    "school_id": "65b0e6293e9f76a9694d84b4",
    "trustee_id": "65b0e552dd319500a9b41c5ba",
    "student_info": {
      "name": "John Doe",
      "id": "STU001",
      "email": "john.doe@school.edu"
    },
    "amount": 5000,
    "gateway_name": "PhonePe"
  }'
```

## 🔧 Configuration

### Payment Gateway Credentials
The application uses the following test credentials:
- **PG Key**: `edvtest01`
- **API Key**: Provided in environment variables
- **School ID**: `65b0e6293e9f76a9694d84b4`

### Sample Data
The application includes realistic sample transaction data for testing:
- 10 sample transactions with various payment statuses
- Authentic payment gateway responses
- Real bank reference formats
- Multiple payment modes (UPI, Net Banking, Cards, Wallet)

## 🧪 Testing

### Using the Application
1. **Dashboard**: View overall transaction statistics and trends
2. **Filter Transactions**: Use the search and filter options to find specific transactions
3. **School View**: Navigate to "School Transactions" to view school-specific data
4. **Status Check**: Use "Status Check" to verify individual transaction status
5. **Theme Toggle**: Switch between light and dark modes using the sidebar toggle

### Sample Transaction IDs for Testing
You can test the status checker with these sample custom order IDs:
- `ORD-1706123456-ABC123`
- `ORD-1706123457-DEF456`
- Any custom_order_id from the transactions table

## 🛡️ Security Features

- **JWT Authentication**: Secure API endpoint access
- **Input Validation**: Comprehensive request validation using Zod
- **Error Handling**: Consistent error responses without sensitive data exposure
- **CORS Configuration**: Proper cross-origin resource sharing setup

## 🌟 Technology Stack

**Frontend:**
- React 18
- TypeScript
- Tailwind CSS
- shadcn/ui components
- TanStack Query
- Wouter (routing)
- Axios

**Backend:**
- Node.js
- Express.js
- TypeScript
- JWT
- Axios
- Zod (validation)

**Development:**
- Vite
- ESBuild
- Hot Module Replacement

## 📁 Project Structure

```
├── client/
│   ├── src/
│   │   ├── components/
│   │   │   ├── dashboard/     # Dashboard components
│   │   │   ├── layout/        # Layout components
│   │   │   ├── modals/        # Modal dialogs
│   │   │   └── ui/            # shadcn/ui components
│   │   ├── pages/             # Route pages
│   │   ├── lib/               # Utilities and API client
│   │   └── types/             # TypeScript type definitions
├── server/
│   ├── index.ts               # Server entry point
│   ├── routes.ts              # API route definitions
│   └── storage.ts             # Data storage layer
├── shared/
│   └── schema.ts              # Shared TypeScript schemas
└── README.md
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License.

## 📞 Support

For support and questions, please refer to the project documentation or create an issue in the repository.
##Output
<img width="1422" height="762" alt="Screenshot 2025-09-09 at 5 25 21 PM" src="https://github.com/user-attachments/assets/1f26bfd8-1da5-44ed-aa4f-df8ee33a1701" />
<img width="1411" height="726" alt="Screenshot 2025-09-09 at 5 26 50 PM" src="https://github.com/user-attachments/assets/ed95dca6-ac52-43b9-b512-888df6198f0c" />
<img width="1440" height="705" alt="Screenshot 2025-09-09 at 5 26 24 PM" src="https://github.com/user-attachments/assets/2b14290c-82d3-4912-85f9-202460e271ab" />
<img width="1407" height="735" alt="Screenshot 2025-09-09 at 5 26 42 PM" src="https://github.com/user-attachments/assets/8258b65b-062f-4b6d-99c8-835730cd7c81" />
<img width="1440" height="689" alt="Screenshot 2025-09-09 at 5 36 58 PM" src="https://github.com/user-attachments/assets/410a770e-497d-41a8-aeae-09e5e4288045" />

