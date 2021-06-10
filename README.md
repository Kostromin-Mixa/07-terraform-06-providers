7.6. Написание собственных провайдеров для Terraform

1.
- resource и data_source:
https://github.com/hashicorp/terraform-provider-aws/blob/31bf342ed9d61ebb7c88f6ae7feda004bc377c25/aws/provider.go#L186
https://github.com/hashicorp/terraform-provider-aws/blob/31bf342ed9d61ebb7c88f6ae7feda004bc377c25/aws/provider.go#L447

2.
- Конфликтный параметр:
https://github.com/hashicorp/terraform-provider-aws/blob/31bf342ed9d61ebb7c88f6ae7feda004bc377c25/aws/resource_aws_sqs_queue.go#L99

"name": {
			Type:          schema.TypeString,
			Optional:      true,
			Computed:      true,
			ForceNew:      true,
			ConflictsWith: []string{"name_prefix"},
		},

- Регулярное выражение, максимальная длина имени:
https://github.com/hashicorp/terraform-provider-aws/blob/31bf342ed9d61ebb7c88f6ae7feda004bc377c25/aws/resource_aws_sqs_queue.go#L405

var re *regexp.Regexp

		if fifoQueue {
			re = regexp.MustCompile(`^[a-zA-Z0-9_-]{1,75}\.fifo$`)
		} else {
			re = regexp.MustCompile(`^[a-zA-Z0-9_-]{1,80}$`)
		}
