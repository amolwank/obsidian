Provisioners in **Terraform** are a way to execute scripts or commands **on a resource after it is created or destroyed**. They act like a "last-mile" configuration step.

🔹 **Key Points about Provisioners:**
- Used when you need to run scripts or commands on a resource (e.g., EC2 instance) after Terraform creates or destroys it.
- They are not recommended as the primary way to configure resources (better to use tools like Ansible, Chef, Puppet, or cloud-init).
- Provisioners should be used only when other options are not possible.
---
### ✅ Types of Provisioners:

1. **file**
    
    - Uploads files or directories to a remote machine.
```
provisioner "file" {
  source      = "script.sh"
  destination = "/tmp/script.sh"
}
```
2. **local-exec**

- Runs a command **on the machine where Terraform is executed**.

```
provisioner "local-exec" {
  command = "echo Hello from local"
}
```
3. **remote-exec**

- Runs commands **on the remote resource** (via SSH or WinRM).

```
provisioner "remote-exec" {
  inline = [
    "sudo apt-get update",
    "sudo apt-get install -y nginx"
  ]
}
```

### ✅ Connection Block (for remote provisioners)
When using `file` or `remote-exec`, you must define how Terraform connects:
```
connection {
  type     = "ssh"
  user     = "ubuntu"
  private_key = file("~/.ssh/id_rsa")
  host     = self.public_ip
}
```

---

### ✅ When Provisioners Run:

- **Creation-time provisioners** → Run after resource creation.
- **Destroy-time provisioners** → Run before resource is destroyed (use `when = destroy`).

---

### ⚠️ Best Practice:

- Avoid relying heavily on provisioners. 
- Use **cloud-init**, **Ansible**, **Packer**, or built-in user data scripts for configuration.
- Provisioners should be a fallback, not the main method.