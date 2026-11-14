# bounce-back-game
gameeee
using UnityEngine;

public class PlayerMovement2D : MonoBehaviour
{
    private Rigidbody2D rb;
    public float moveSpeed = 8f;
    public float jumpForce = 12f;
    private float horizontalInput;
    
    // Kiểm tra xem nhân vật có đang đứng trên mặt đất không
    public Transform groundCheck;
    public LayerMask groundLayer;
    private bool isGrounded;

    void Start()
    {
        rb = GetComponent<Rigidbody2D>();
    }

    void Update()
    {
        // Nhận phím điều hướng trái/phải (A/D hoặc mũi tên)
        horizontalInput = Input.GetAxisRaw("Horizontal");

        // Kiểm tra chạm đất
        isGrounded = Physics2D.OverlapCircle(groundCheck.position, 0.2f, groundLayer);

        // Nhảy khi nhấn phím Space và đang ở trên mặt đất
        if (Input.GetButtonDown("Jump") && isGrounded)
        {
            rb.velocity = new Vector2(rb.velocity.x, jumpForce);
        }
    }

    void FixedUpdate()
    {
        // Di chuyển ngang
        rb.velocity = new Vector2(horizontalInput * moveSpeed, rb.velocity.y);
    }
}
