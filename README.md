# Terraform tutorial from Medium post

You can find the tutorial in this [Medium post](https://blog.gruntwork.io/an-introduction-to-terraform-f17df9c6d180#a9b0)

If you complete the tutorial after running `terraform apply` you should expect the following output:

```terraform
(venv) ubuntu@charm-dev:~/Canonical/terraform$ terraform apply
aws_security_group.instance: Refreshing state... [id=sg-0194f840a2fb39a70]
aws_instance.example: Refreshing state... [id=i-04b617fc2ec4792f9]

Changes to Outputs:

- public_ip = "18.217.32.146"

You can apply this plan to save these new output values to the Terraform state, without changing any real infrastructure.

Do you want to perform these actions?
Terraform will perform the actions described above.
Only 'yes' will be accepted to approve.

Enter a value: yes

Apply complete! Resources: 0 added, 0 changed, 0 destroyed.

Outputs:

public_ip = "18.217.32.146"
(venv) ubuntu@charm-dev:~/Canonical/terraform$ terraform outputs
Terraform has no command named "outputs". Did you mean "output"?

To see all of Terraform's top-level commands, run:
terraform -help

(venv) ubuntu@charm-dev:~/Canonical/terraform$ terraform output
public_ip = "18.217.32.146"
(venv) ubuntu@charm-dev:~/Canonical/terraform$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
(use "git restore --staged <file>..." to unstage)
new file: README.md
modified: main.tf

(venv) ubuntu@charm-dev:~/Canonical/terraform$ git add -A
(venv) ubuntu@charm-dev:~/Canonical/terraform$ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
(use "git restore --staged <file>..." to unstage)
new file: README.md
modified: main.tf

(venv) ubuntu@charm-dev:~/Canonical/terraform$ git commit -m "Adds web server, variables, security group and outputs"
[main 33b18a0] Adds web server, variables, security group and outputs
2 files changed, 35 insertions(+), 2 deletions(-)
create mode 100644 README.md
(venv) ubuntu@charm-dev:~/Canonical/terraform$ git push origin main
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 6 threads
Compressing objects: 100% (4/4), done.
Writing objects: 100% (4/4), 992 bytes | 141.00 KiB/s, done.
Total 4 (delta 0), reused 0 (delta 0)
To github.com:sanchezfdezjavier/terraform-tutorial.git
533e124..33b18a0 main -> main
(venv) ubuntu@charm-dev:~/Canonical/terraform$ terraform apply
╷
│ Error: Reference to undeclared resource
│
│ on main.tf line 60, in resource "aws_autoscaling_group" "example":
│ 60: target_group_arns = [aws_lb_target_group.example.arn]
│
│ A managed resource "aws_lb_target_group" "example" has not been declared in the root module.
╵
(venv) ubuntu@charm-dev:~/Canonical/terraform$ terraform apply
╷
│ Error: Reference to undeclared resource
│
│ on main.tf line 60, in resource "aws_autoscaling_group" "example":
│ 60: target_group_arns = [aws_alb_target_group.example.arn]
│
│ A managed resource "aws_alb_target_group" "example" has not been declared in the root module.
╵
(venv) ubuntu@charm-dev:~/Canonical/terraform$ terraform apply
╷
│ Error: Unsupported argument
│
│ on main.tf line 71, in resource "aws_autoscaling_group" "example":
│ 71: propagate_at_launch = true
│
│ An argument named "propagate_at_launch" is not expected here.
╵
(venv) ubuntu@charm-dev:~/Canonical/terraform$ terraform apply
data.aws_vpc.default: Reading...
aws_security_group.instance: Refreshing state... [id=sg-0194f840a2fb39a70]
aws_instance.example: Refreshing state... [id=i-04b617fc2ec4792f9]
data.aws_vpc.default: Read complete after 1s [id=vpc-0328e3cf561b33d3d]
data.aws_subnets.default: Reading...
data.aws_subnets.default: Read complete after 0s [id=us-east-2]

Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:

- create

Terraform will perform the following actions:

# aws_autoscaling_group.example will be created

- resource "aws_autoscaling_group" "example" {

  - arn = (known after apply)
  - availability_zones = (known after apply)
  - default_cooldown = (known after apply)
  - desired_capacity = (known after apply)
  - force_delete = false
  - force_delete_warm_pool = false
  - health_check_grace_period = 300
  - health_check_type = "ELB"
  - id = (known after apply)
  - launch_configuration = (known after apply)
  - max_size = 4
  - metrics_granularity = "1Minute"
  - min_size = 2
  - name = (known after apply)
  - name_prefix = (known after apply)
  - protect_from_scale_in = false
  - service_linked_role_arn = (known after apply)
  - target_group_arns = (known after apply)
  - vpc_zone_identifier = [
    - "subnet-0386fd14b41e9891d",
    - "subnet-0ec259d9f201e9399",
    - "subnet-0f6f054cbe432efa4",
      ]
  - wait_for_capacity_timeout = "10m"

  - tag { + key = "Name" + propagate_at_launch = true + value = "terraform-asg-example"
    }
    }

# aws_launch_configuration.example will be created

- resource "aws_launch_configuration" "example" {

  - arn = (known after apply)
  - associate_public_ip_address = (known after apply)
  - ebs_optimized = (known after apply)
  - enable_monitoring = true
  - id = (known after apply)
  - image_id = "ami-0fb653ca2d3203ac1"
  - instance_type = "t2.micro"
  - key_name = (known after apply)
  - name = (known after apply)
  - name_prefix = (known after apply)
  - security_groups = [
    - "sg-0194f840a2fb39a70",
      ]
  - user_data = "c765373c563b260626d113c4a56a46e8a8c5ca33"

  - ebs_block_device {

    - delete_on_termination = (known after apply)
    - device_name = (known after apply)
    - encrypted = (known after apply)
    - iops = (known after apply)
    - no_device = (known after apply)
    - snapshot_id = (known after apply)
    - throughput = (known after apply)
    - volume_size = (known after apply)
    - volume_type = (known after apply)
      }

  - metadata_options {

    - http_endpoint = (known after apply)
    - http_put_response_hop_limit = (known after apply)
    - http_tokens = (known after apply)
      }

  - root_block_device { + delete_on_termination = (known after apply) + encrypted = (known after apply) + iops = (known after apply) + throughput = (known after apply) + volume_size = (known after apply) + volume_type = (known after apply)
    }
    }

# aws_lb.example will be created

- resource "aws_lb" "example" {

  - arn = (known after apply)
  - arn_suffix = (known after apply)
  - desync_mitigation_mode = "defensive"
  - dns_name = (known after apply)
  - drop_invalid_header_fields = false
  - enable_deletion_protection = false
  - enable_http2 = true
  - enable_waf_fail_open = false
  - id = (known after apply)
  - idle_timeout = 60
  - internal = (known after apply)
  - ip_address_type = (known after apply)
  - load_balancer_type = "application"
  - name = "terraform-asg-example"
  - preserve_host_header = false
  - security_groups = (known after apply)
  - subnets = [
    - "subnet-0386fd14b41e9891d",
    - "subnet-0ec259d9f201e9399",
    - "subnet-0f6f054cbe432efa4",
      ]
  - tags_all = (known after apply)
  - vpc_id = (known after apply)
  - zone_id = (known after apply)

  - subnet_mapping { + allocation_id = (known after apply) + ipv6_address = (known after apply) + outpost_id = (known after apply) + private_ipv4_address = (known after apply) + subnet_id = (known after apply)
    }
    }

# aws_lb_listener.http will be created

- resource "aws_lb_listener" "http" {

  - arn = (known after apply)
  - id = (known after apply)
  - load_balancer_arn = (known after apply)
  - port = 80
  - protocol = "HTTP"
  - ssl_policy = (known after apply)
  - tags_all = (known after apply)

  - default_action { + order = (known after apply) + type = "fixed-response"

          + fixed_response {
              + content_type = "text/plain"
              + message_body = "404: Not Found"
              + status_code  = "404"
            }
        }

    }

# aws_lb_listener_rule.asg will be created

- resource "aws_lb_listener_rule" "asg" {

  - arn = (known after apply)
  - id = (known after apply)
  - listener_arn = (known after apply)
  - priority = 100
  - tags_all = (known after apply)

  - action {

    - order = (known after apply)
    - target_group_arn = (known after apply)
    - type = "forward"
      }

  - condition {

          + path_pattern {
              + values = [
                  + "*",
                ]
            }
        }

    }

# aws_lb_target_group.asg will be created

- resource "aws_lb_target_group" "asg" {

  - arn = (known after apply)
  - arn_suffix = (known after apply)
  - connection_termination = false
  - deregistration_delay = "300"
  - id = (known after apply)
  - ip_address_type = (known after apply)
  - lambda_multi_value_headers_enabled = false
  - load_balancing_algorithm_type = (known after apply)
  - name = "terraform-asg-example"
  - port = 8080
  - preserve_client_ip = (known after apply)
  - protocol = "HTTP"
  - protocol_version = (known after apply)
  - proxy_protocol_v2 = false
  - slow_start = 0
  - tags_all = (known after apply)
  - target_type = "instance"
  - vpc_id = "vpc-0328e3cf561b33d3d"

  - health_check {

    - enabled = true
    - healthy_threshold = 2
    - interval = 15
    - matcher = "200"
    - path = "/"
    - port = "traffic-port"
    - protocol = "HTTP"
    - timeout = 3
    - unhealthy_threshold = 2
      }

  - stickiness {

    - cookie_duration = (known after apply)
    - cookie_name = (known after apply)
    - enabled = (known after apply)
    - type = (known after apply)
      }

  - target_failover { + on_deregistration = (known after apply) + on_unhealthy = (known after apply)
    }
    }

# aws_security_group.alb will be created

- resource "aws_security_group" "alb" {
  - arn = (known after apply)
  - description = "Managed by Terraform"
  - egress = [
    - { + cidr_blocks = [
      - "0.0.0.0/0",
        ] + description = "" + from_port = 0 + ipv6_cidr_blocks = [] + prefix_list_ids = [] + protocol = "-1" + security_groups = [] + self = false + to_port = 0
        },
        ]
  - id = (known after apply)
  - ingress = [
    - { + cidr_blocks = [
      - "0.0.0.0/0",
        ] + description = "" + from_port = 80 + ipv6_cidr_blocks = [] + prefix_list_ids = [] + protocol = "tcp" + security_groups = [] + self = false + to_port = 80
        },
        ]
  - name = "terraform-example-alb"
  - name_prefix = (known after apply)
  - owner_id = (known after apply)
  - revoke_rules_on_delete = false
  - tags_all = (known after apply)
  - vpc_id = (known after apply)
    }

Plan: 7 to add, 0 to change, 0 to destroy.

Changes to Outputs:
~ public_ip = "18.217.32.146" -> (known after apply)

Do you want to perform these actions?
Terraform will perform the actions described above.
Only 'yes' will be accepted to approve.

Enter a value: yes

aws_launch_configuration.example: Creating...
aws_lb_target_group.asg: Creating...
aws_security_group.alb: Creating...
aws_launch_configuration.example: Creation complete after 1s [id=terraform-20221108164652702800000001]
aws_lb_target_group.asg: Creation complete after 1s [id=arn:aws:elasticloadbalancing:us-east-2:872104920976:targetgroup/terraform-asg-example/3a230b931df26410]
aws_autoscaling_group.example: Creating...
aws_security_group.alb: Creation complete after 3s [id=sg-0b722212e439bec37]
aws_lb.example: Creating...
aws_autoscaling_group.example: Still creating... [10s elapsed]
aws_lb.example: Still creating... [10s elapsed]
aws_autoscaling_group.example: Still creating... [20s elapsed]
aws_lb.example: Still creating... [20s elapsed]
aws_autoscaling_group.example: Still creating... [30s elapsed]
aws_lb.example: Still creating... [30s elapsed]
aws_autoscaling_group.example: Creation complete after 40s [id=terraform-20221108164654316200000002]
aws_lb.example: Still creating... [40s elapsed]
aws_lb.example: Still creating... [50s elapsed]
aws_lb.example: Still creating... [1m0s elapsed]
aws_lb.example: Still creating... [1m10s elapsed]
aws_lb.example: Still creating... [1m20s elapsed]
aws_lb.example: Still creating... [1m31s elapsed]
aws_lb.example: Still creating... [1m41s elapsed]
aws_lb.example: Still creating... [1m51s elapsed]
aws_lb.example: Still creating... [2m1s elapsed]
aws_lb.example: Creation complete after 2m6s [id=arn:aws:elasticloadbalancing:us-east-2:872104920976:loadbalancer/app/terraform-asg-example/ddbe18708028cb0a]
aws_lb_listener.http: Creating...
aws_lb_listener.http: Creation complete after 1s [id=arn:aws:elasticloadbalancing:us-east-2:872104920976:listener/app/terraform-asg-example/ddbe18708028cb0a/77f6458aff4a297c]
aws_lb_listener_rule.asg: Creating...
aws_lb_listener_rule.asg: Creation complete after 0s [id=arn:aws:elasticloadbalancing:us-east-2:872104920976:listener-rule/app/terraform-asg-example/ddbe18708028cb0a/77f6458aff4a297c/ab57def2e3a9fc6a]

Apply complete! Resources: 7 added, 0 changed, 0 destroyed.

Outputs:

public_ip = "terraform-asg-example-517030553.us-east-2.elb.amazonaws.com"

```
