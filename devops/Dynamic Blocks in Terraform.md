Dynamic blocks **Quick Summary:**
?
Dynamic blocks are a terraform feature that allows you to dynamically generate multiple nested configuration blocks based on variables or expressions, eliminating code duplication and making configurations more reusable and maintainable.

**Definition and Purpose:**
Dynamic blocks in Terraform solve the problem of repetitive configuration blocks. Instead of manually writing multiple similar blocks, you can define them dynamically using loops.

**Basic Syntax:**

```
dynamic "block_name" {     # The nested block type to generate
	for_each = collection  # The list/map to iterate over
	content {              # The Template for each block
        # Configuration using each.value or each.key
	}
}
```

**Example 1: Security Group Rules:**
"I recently used dynamic blocks for AWS security groups. Instead of hardcoding ingress rules, i made them dynamic."

```
variable "ingress_rules" {
  type = list(object({
    port        = number
    protocol    = string
    cidr_blocks = list(string)
  }))
  default = [
    { port = 80, protocol = "tcp", cidr_blocks = ["0.0.0.0/0"] },
    { port = 443, protocol = "tcp", cidr_blocks = ["0.0.0.0/0"] }
  ]
}

resource "aws_security_group" "web" {
  dynamic "ingress" {
    for_each = var.ingress_rules
    content {
      from_port   = ingress.value.port
      to_port     = ingress.value.port
      protocol    = ingress.value.protocol

      cidr_blocks = ingress.value.cidr_blocks
    }
  }
}
```

## **🎓 Interview Cheat Sheet**

### **Key Points to Remember:**

1. **Definition**: Dynamic generation of nested blocks
2. **Syntax**: `dynamic "block_name" { for_each = collection; content { ... } }`
3. **Use Case**: Eliminate repetitive nested blocks
4. **Benefits**: DRY, maintainable, reusable code
5. **Real Example**: Security group rules, tags, listeners
    

### **Sample Q&A Flow:**

**Interviewer**: "What are dynamic blocks in Terraform?"  
**You**: "They're a feature that lets you dynamically generate multiple nested configuration blocks using loops. For example, instead of writing 10 separate security group rules, you can define them once and iterate over a list of rule definitions."


------------------------------------------------------------------------

Video Ref: https://www.youtube.com/watch?v=VwCVP5AYUuM


#flashcards 
