## 🔹 How to Handle Terraform Plan Reviews in PRs

### 1. **CI/CD Integration**

- Use **GitHub Actions / GitLab CI / Jenkins** to run `terraform plan` automatically when a PR is opened.
    
- Example GitHub Actions step:

```
- name: Terraform Plan
  run: terraform plan -out=tfplan

```

---

### 2. **Post Plan Output in PR**

- The pipeline posts the **plan summary** as a comment in the PR, so reviewers see what resources will be created/updated/destroyed.
    
- Example with GitHub Actions:


```
- name: Comment Plan Output
  uses: actions/github-script@v7
  with:
    script: |
      const fs = require('fs');
      const plan = fs.readFileSync('plan.out', 'utf8');
      github.rest.issues.createComment({
        issue_number: context.issue.number,
        owner: context.repo.owner,
        repo: context.repo.repo,
        body: `Terraform Plan:\n\`\`\`\n${plan}\n\`\`\``
      });
```

---

### 3. **Human Review**

- Reviewers check:
    
    - Are there unexpected resource deletions?
        
    - Are tagging/standards followed?
        
    - Are costs impacted (use `infracost` integration for estimates)?
        

---

### 4. **Approval Workflow**

- Only after plan review + PR approval → merge → pipeline runs `terraform apply`.
    
- For **prod**, require extra manual approval step.
    

---

### 5. **Best Practices**

- **Mask sensitive outputs** (DB passwords, secrets).
    
- Keep plan diffs small (modularize code to avoid giant plans).
    
- Use **policy checks** (OPA/Sentinel) to enforce rules automatically.
    

---

## 🔹 Interview-Ready Answer (45 sec)

_"In our setup, every pull request triggers a Terraform plan via GitHub Actions. The plan output is posted as a PR comment so reviewers can see exactly what infra changes will happen. Reviewers validate whether the changes are intentional, safe, and cost-effective, sometimes using tools like Infracost. Only after approval is the PR merged, and the pipeline then runs `terraform apply`. This ensures peer review, prevents surprises, and keeps infra changes auditable."_