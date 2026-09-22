# Ansible role: QEMU Guest Agent (Proxmox)

Ansible role pro instalaci a správu nástrojů pro hosty v prostředí Proxmox VE (KVM/QEMU) ve formě balíčku `qemu-guest-agent`.

## Co role provádí

Role se provede pouze na hostech, u kterých Ansible zjistí:

```yaml
ansible_facts["virtualization_type"] in ["kvm", "qemu"]
```

Pokud je role povolená, provede následující kroky:

- nainstaluje balíček `qemu-guest-agent`,
- zajistí spuštění služby `qemu-guest-agent`,
- nastaví službu `qemu-guest-agent` tak, aby se spouštěla po startu systému.
Na hostech, které nejsou virtualizované pod KVM/QEMU, se úlohy přeskočí.

## Podporované systémy

- Red Hat Enterprise Linux a kompatibilní distribuce: 8, 9
- Debian: Bullseye, Bookworm
- Ubuntu: Focal, Jammy

## Proměnné

### `qemu_guest_agent_enabled`
Určuje, zda má role instalaci a správu QEMU Guest Agenta provádět. Výchozí hodnota je `false`.

```yaml
qemu_guest_agent_enabled: true
```

## Použití
Role lze přidat do playbooku takto:

```yaml
- name: Instalace QEMU Guest Agent (Proxmox Tools)
  hosts: all
  become: true

  vars:
      qemu_guest_agent_enabled: true

  roles:
      - ansible-tul.qemu-guest-agent
```

Případně lze proměnnou nastavit v inventáři:

```yaml
qemu_guest_agent_enabled: true
```

## Example `requirements.yml` for Ansible site

```yaml
roles:
  - name: ansible-tul.qemu-guest-agent
    src: https://github.com/ansible-tul/ansible-role-qemu-guest-agent.git
```

Při použití role musí mít cílový host dostupný balíčkovací systém a oprávnění pro instalaci balíčků a správu systémových služeb.

## Požadavky

- Ansible 2.12 nebo novější
- oprávnění `become` pro instalaci balíčků a správu služby
