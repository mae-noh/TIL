CREATE TABLE `PAYMENT` (
	`payment_id`	int	NOT NULL,
	`payment`	varchar(45)	NULL,
	`price_per_person`	boolean	NULL	COMMENT 'x',
	`price_per_hour`	boolean	NULL	COMMENT 'x',
	`final_payment`	boolean	NULL,
	`cost_payment`	boolean	NULL,
	`created_user`	int	NULL,
	`created_dt`	date	NULL,
	`modified_user`	int	NULL,
	`modified_at`	date	NULL,
	`reservation_id`	int	NOT NULL,
	`product_id`	int8	NOT NULL	COMMENT 'phone'
);

CREATE TABLE `RESERVATION` (
	`reservation_id`	int	NOT NULL,
	`reservation_date`	varchar(45)	NULL,
	`use_date`	VARCHAR(255)	NULL,
	`check_in_date`	VARCHAR(255)	NULL,
	`check_out_date`	VARCHAR(255)	NULL,
	`path`	VARCHAR(255)	NULL,
	`category`	VARCHAR(255)	NULL,
	`term`	VARCHAR(255)	NULL,
	`Field3`	VARCHAR(255)	NULL,
	`use_duration`	VARCHAR(255)	NULL,
	`Field9`	VARCHAR(255)	NULL,
	`Field8`	VARCHAR(255)	NULL,
	`Field`	VARCHAR(255)	NULL,
	`created_user`	int	NULL,
	`created_at`	date	NULL,
	`modified_user`	int	NULL,
	`modified_at`	date	NULL,
	`guest_id`	int8	NOT NULL	COMMENT 'phone'
);

CREATE TABLE `GUEST` (
	`guest_id`	int8	NOT NULL	COMMENT 'phone',
	`name`	varchar(30)	NULL
);

CREATE TABLE `REFUND` (
	`refund_id`	int	NOT NULL,
	`name`	varchar(45)	NULL,
	`refund_date`	boolean	NULL,
	`created_user`	int	NULL,
	`created_dt`	date	NULL,
	`modified_user`	int	NULL,
	`modified_at`	date	NULL,
	`payment_id`	int	NOT NULL
);

CREATE TABLE `SPACE` (
	`space_id`	int8	NOT NULL	COMMENT 'phone',
	`name`	varchar(30)	NULL,
	`capacity`	int	NULL
);

CREATE TABLE `PRODUCT` (
	`product_id`	int8	NOT NULL	COMMENT 'phone',
	`name`	varchar(30)	NULL,
	`price`	VARCHAR(255)	NULL,
	`category`	VARCHAR(255)	NULL,
	`space_id`	int8	NOT NULL	COMMENT 'phone',
	`Field`	VARCHAR(255)	NULL
);

CREATE TABLE `REVIEW` (
	`review_id`	int	NOT NULL,
	`content`	varchar(45)	NULL,
	`review_date`	boolean	NULL,
	`created_user`	int	NULL,
	`created_date`	date	NULL,
	`modified_user`	int	NULL,
	`modified_at`	date	NULL,
	`guest_id`	int8	NOT NULL	COMMENT 'phone',
	`reservation_id`	int	NOT NULL
);

ALTER TABLE `PAYMENT` ADD CONSTRAINT `PK_PAYMENT` PRIMARY KEY (
	`payment_id`
);

ALTER TABLE `RESERVATION` ADD CONSTRAINT `PK_RESERVATION` PRIMARY KEY (
	`reservation_id`
);

ALTER TABLE `GUEST` ADD CONSTRAINT `PK_GUEST` PRIMARY KEY (
	`guest_id`
);

ALTER TABLE `REFUND` ADD CONSTRAINT `PK_REFUND` PRIMARY KEY (
	`refund_id`
);

ALTER TABLE `SPACE` ADD CONSTRAINT `PK_SPACE` PRIMARY KEY (
	`space_id`
);

ALTER TABLE `PRODUCT` ADD CONSTRAINT `PK_PRODUCT` PRIMARY KEY (
	`product_id`
);

ALTER TABLE `REVIEW` ADD CONSTRAINT `PK_REVIEW` PRIMARY KEY (
	`review_id`
);

