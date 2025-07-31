<h3>****The app source code is cloned from from https://github.com/burakorkmez/mern-ecommerce.git ****<h3>

This is a full-featured **E-commerce application** built using the **MERN stack (MongoDB, Express, React, Node.js)**.
The project includes authentication, product management, shopping cart, payments, and more.


For Dev environment
Dockerfile are in each folder and docker-compose.yml file is in root folder
We have change few things for dev env,
In backend,
1. In server.js, line 42 add 0.0.0.0
   <pre>app.listen(PORT, '0.0.0.0' , () => { </pre>
   We don't want it to listen only on localhost.

   
3. Add .env file
      <pre> 
      PORT=5000
      MONGO_URI=mongodb://mongo:27017/mydatabase
      UPSTASH_REDIS_URL=redis://redis:6379
      
      ACCESS_TOKEN_SECRET=dev_access_secret
      REFRESH_TOKEN_SECRET=dev_refresh_secret
      
      CLOUDINARY_CLOUD_NAME=dummy
      CLOUDINARY_API_KEY=123456
      CLOUDINARY_API_SECRET=abcdef
      
      STRIPE_SECRET_KEY=sk_test_dummy
      CLIENT_URL=http://frontend:5173
      NODE_ENV=development
      </pre>



In frontend,
1.Change vite.config.js

      export default defineConfig({
      	plugins: [react()],
      	server: {
      		host: '0.0.0.0',
      		port: 5173,
      		proxy: {
      			"/api": {
      				target: "http://backend:5000", // <--- use backend service name here
      				changeOrigin: true,
      			},
      		},
      	},
      });


2.Add .env as below

    VITE_BACKEND_URL=/api

After changes run "docker compose up"

<h2>For Production use Dockerfile.prod and docker-compose-prod.yml</h2>  
For prod,Ignore frontend .env and for real deployment use real TOKENS and KEYS 
