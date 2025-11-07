# Smart Flows Client PoC

A simple client application that demonstrates Supabase authentication with Google OAuth and n8n workflow integration.

## Setup Instructions

### 1. Supabase Configuration

1. In your Supabase dashboard, go to Authentication > Providers
2. Enable Google OAuth provider
3. Add your domain to the allowed redirect URLs
4. Copy your anon key and replace `YOUR_SUPABASE_ANON_KEY` in `index.html`

### 2. n8n Workflow Setup

1. Import the `flow.json` file into your n8n instance at https://flows.smartfront.cl
2. Configure Supabase credentials in n8n:
   - Go to Credentials > Add Credential > Supabase API
   - Add your Supabase URL and service role key
   - Name it "Supabase API"

### 3. Database Setup

The workflow assumes your Supabase database already has the required tables (users, runs, etc.) as described in your schema.

### 4. Running the Application

1. Serve the `index.html` file using a local web server:
   ```bash
   # Using Python
   python -m http.server 8000
   
   # Using Node.js
   npx serve .
   ```

2. Open your browser and navigate to the local server
3. Click "Sign in with Google" to authenticate
4. Enter text and click "Execute Workflow" to test the n8n integration

## Features

- Google OAuth authentication via Supabase
- JWT token handling
- Clean, professional UI
- Real-time workflow execution
- Error handling and user feedback
- Automatic user creation in database
- Run logging for analytics

## Workflow Details

The n8n workflow (`flow.json`) includes:

1. **Webhook Trigger**: Receives POST requests from the client
2. **User Check**: Verifies if user exists in Supabase database
3. **User Creation**: Creates new user if doesn't exist
4. **Text Processing**: Simple text transformation (converts to uppercase, counts words)
5. **Run Logging**: Records workflow execution in runs table
6. **Response**: Returns processed data to client

## Customization

- Modify the text processing logic in the "Process Text" node
- Add additional workflow steps as needed
- Customize the UI styling in `index.html`
- Add more sophisticated error handling
- Implement organization and membership logic

## Security Notes

- Replace the placeholder Supabase anon key with your actual key
- Ensure proper RLS policies are set up in Supabase
- Use HTTPS in production
- Validate JWT tokens in n8n workflow if needed