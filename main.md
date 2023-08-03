### create address table with id and address as char.

```
CREATE TABLE public.address (
	id uuid NOT NULL DEFAULT uuid_generate_v4(),
	"data" varchar NOT NULL,
	CONSTRAINT address_pk PRIMARY KEY (id)
);
ALTER TABLE public.address ADD CONSTRAINT address_fk FOREIGN KEY (id) REFERENCES public."user"(id) ON DELETE CASCADE ON UPDATE CASCADE;

```

### create category table with product id nad category name

```
CREATE TABLE public.category (
	id uuid NOT NULL,
	category_id uuid NOT NULL,
	uuid uuid NOT NULL DEFAULT uuid_generate_v4()
);
CREATE INDEX category_c_name_idx ON public.category USING btree (category_id);
ALTER TABLE public.category ADD CONSTRAINT category_fk_2 FOREIGN KEY (category_id) REFERENCES category_product(id);

```

### category_product joint table

```
CREATE TABLE public.category_product (
	product_id uuid NOT NULL DEFAULT uuid_generate_v4(),
	category_name varchar NOT NULL,
	id uuid NOT NULL DEFAULT uuid_generate_v4(),
	CONSTRAINT category_product_pk PRIMARY KEY (id),
	CONSTRAINT category_product_un UNIQUE (category_name)
);
ALTER TABLE public.catrgory_product ADD CONSTRAINT product_catrgory_fk_2 FOREIGN KEY (product_id) REFERENCES product(id);

```

### Create order table with user and address details with price

```
-- public."order" definition

-- Drop table

-- DROP TABLE public."order";

CREATE TABLE public."order" (
	user_id uuid NOT NULL,
	address_id uuid NOT NULL,
	order_id uuid NOT NULL DEFAULT uuid_generate_v4(),
	price varchar NOT NULL,
	CONSTRAINT orders_pk PRIMARY KEY (order_id)
);
ALTER TABLE public.order ADD CONSTRAINT order_fk FOREIGN KEY (address_id) REFERENCES "address"(id) ON UPDATE CASCADE ON DELETE CASCADE;


```
### product table with product price name and description

```
-- public.product definition

-- Drop table

-- DROP TABLE public.product;

CREATE TABLE public.product (
	"name" varchar NOT NULL,
	description varchar NOT NULL,
	price varchar NOT NULL,
	sku uuid NOT NULL DEFAULT uuid_generate_v4(),
	CONSTRAINT products_pk PRIMARY KEY (sku)
);

CREATE INDEX products_name_idx ON public.product USING btree (name);4
```
### product order joint table 

```
CREATE TABLE public."order" (
	user_id uuid NOT NULL,
	address_id uuid NOT NULL,
	order_id uuid NOT NULL DEFAULT uuid_generate_v4(),
	price float8 NOT NULL,
	CONSTRAINT orders_pk PRIMARY KEY (order_id)
);
ALTER TABLE public.order_product ADD CONSTRAINT product_order_fk FOREIGN KEY (order_id) REFERENCES "order"(order_id);
ALTER TABLE public.order_product ADD CONSTRAINT product_order_fk_2 FOREIGN KEY (product_id) REFERENCES product(id);


```
### Creating User table
```
CREATE TABLE public."user" (
	"name" varchar NOT NULL,
	address_id varchar NOT NULL,
	phone varchar NOT NULL,
	email varchar NOT NULL,
	passord varchar NOT NULL,
	id uuid NOT NULL DEFAULT uuid_generate_v4(),
	CONSTRAINT user_pk PRIMARY KEY (id)
);
```
