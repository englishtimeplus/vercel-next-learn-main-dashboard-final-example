CREATE TABLE customers (
    id SERIAL PRIMARY KEY,
    name VARCHAR(255) NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    image_url TEXT
);


CREATE TABLE invoices (
    id SERIAL PRIMARY KEY,
    customer_id INTEGER REFERENCES customers(id) ON DELETE CASCADE,
    amount INTEGER NOT NULL,  -- Amount in cents to avoid floating point issues
    status VARCHAR(50) CHECK (status IN ('paid', 'pending', 'cancelled')) NOT NULL,
    date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE revenue (
    id SERIAL PRIMARY KEY,
    total_amount INTEGER NOT NULL,  -- Total revenue in cents
    date TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
 

CREATE TABLE public."user" (
	id uuid DEFAULT gen_random_uuid() NOT NULL,
	"name" text NOT NULL,
	email text NOT NULL,
	"role" text DEFAULT 'user'::text NOT NULL,
	"password" text NULL,
	"emailVerified" timestamp NULL,
	image text NULL,
	address json NULL,
	"paymentMethod" text NULL,
	"createdAt" timestamp DEFAULT now() NULL,
	CONSTRAINT user_pkey PRIMARY KEY (id)
);
CREATE UNIQUE INDEX user_email_idx ON public."user" USING btree (email);