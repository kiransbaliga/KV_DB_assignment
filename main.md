```

-- public.address definition

-- Drop table

-- DROP TABLE public.address;

CREATE TABLE public.address (
	id uuid NOT NULL DEFAULT uuid_generate_v4(),
	"data" varchar NOT NULL,
	CONSTRAINT address_pk PRIMARY KEY (id)
);

```

```
-- public.category definition

-- Drop table

-- DROP TABLE public.category;

CREATE TABLE public.category (
	p_id uuid NOT NULL,
	c_name varchar NOT NULL
);
CREATE INDEX category_c_name_idx ON public.category USING btree (c_name);

```

```
-- public.category_product definition

-- Drop table

-- DROP TABLE public.category_product;

CREATE TABLE public.category_product (
	id uuid NOT NULL DEFAULT uuid_generate_v4(),
	category_id varchar NOT NULL,
	CONSTRAINT category_product_pk PRIMARY KEY (id)
);
```

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
```

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

```
-- public.product_order definition

-- Drop table

-- DROP TABLE public.product_order;

CREATE TABLE public.product_order (
	order_id uuid NOT NULL,
	product_id uuid NOT NULL,
	count int4 NOT NULL DEFAULT 1,
	tot_price varchar NOT NULL
);

```

```
-- public.product_order foreign keys

ALTER TABLE public.product_order ADD CONSTRAINT product_order_fk FOREIGN KEY (order_id) REFERENCES public."order"(order_id);
ALTER TABLE public.product_order ADD CONSTRAINT product_order_fk_2 FOREIGN KEY (product_id) REFERENCES public.product(sku);

-- public."user" definition

-- Drop table

-- DROP TABLE public."user";

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
